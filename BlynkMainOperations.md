#Blynk main operations

##Virtual Pins
Blynk can control Digital and Analog I/O Pins on you hardware directly. You don't even need to write code for it. 
It's great for blinking LEDs, but often it's just not enough...

We designed Virtual Pins to send **any** data from your microcontroller to the Blynk App and back. 

Anything you connect to your hardware will be able to talk to Blynk.
With Virtual Pins you can send something from the App, process it on microcontroller and then send it back to the smartphone. You can trigger functions, read I2C devices, convert values, control servo and DC motors etc.

Virtual Pins can be used to interface with external libraries (Servo, LCD and others) and implement custom functionality. 

Hardware may send data to the Widgets over the Virtual Pin like this:

```cpp
Blynk.virtualWrite(pin, "abc");
Blynk.virtualWrite(pin, 123);
Blynk.virtualWrite(pin, 12.34);
Blynk.virtualWrite(pin, "hello", 123, 12.34);
```

For more information about virtual pins, [read this](http://docs.blynk.cc/#blynk-firmware-virtual-pins-control)

##Send data from app to hardware
You can send any data from Widgets in the app to your hardware.

All [Controller Widgets](http://docs.blynk.cc/#widgets-controllers) can send data to Virtual Pins on your hardware. 
For example, code below shows how to get values from the Button Widget in the App

```cpp
BLYNK_WRITE(V1) //Button Widget is writing to pin V1
{
  int pinData = param.asInt(); 
}
```
When you press a Button, Blynk App sends ```1``` On the second click - it sends ```0``` 

This is how Button Widget is set up:

<img src="images/button_virtual_1.png" style="width: 200px; height:360px"/>


Full example sketch: [Get Data](https://github.com/blynkkk/blynk-library/blob/master/examples/GettingStarted/GetData/GetData.ino#L24)

###Sending array from Widget 
Some Widgets (e.g Joystick, zeRGBa) have more than one output. 

<img src="images/joystick_merge_mode.png" style="width: 200px; height:360px"/>

This output can be written to Virtual Pin as an array of values. 
On the hardware side - you can get any element of the array [0,1,2...] by using: 

```cpp
BLYNK_WRITE(V1) // Widget WRITEs to Virtual Pin V1
{   
  int x = param[0].asInt(); // getting first value
  int y = param[1].asInt(); // getting second value
  int z = param[N].asInt(); // getting N value
}
```

 **Sketch:** [JoystickTwoAxis](https://github.com/blynkkk/blynk-library/blob/master/examples/Widgets/JoystickTwoAxis/JoystickTwoAxis.ino#L24)

##Get data from hardware
There are two ways of pushing data from your hardware to the Widgets in the app over Virtual Pins.

###Perform requests by Widget
- Using Blynk built-in reading frequency while App is active by setting 'Reading Frequency' parameter to some interval:

<img src="images/frequency_reading_pull.png" style="width: 200px; height:360px"/>

```cpp
BLYNK_READ(V5) // Widget in the app READs Virtal Pin V5 with the certain frequency
{
  // This command writes Arduino's uptime in seconds to Virtual Pin V5
  Blynk.virtualWrite(5, millis() / 1000);
}
```

**Sketch:** [PushDataOnRequest](https://github.com/blynkkk/blynk-library/blob/master/examples/GettingStarted/PushDataOnRequest/PushDataOnRequest.ino#L26)


###Pushing data from hardware
If you need to PUSH sensor or other data from your hardware to Widget, you can write any logic you want. 
Just set the frequency to PUSH mode. Any command that hardware sends to Blynk Cloud is automatically stored on server
and you get this info either with [History Graph](http://docs.blynk.cc/#widgets-displays-history-graph) widget 
or with [HTTP API](http://docs.blynkapi.apiary.io/#reference/0/pin-history-data/get-all-history-data-for-specific-pin).

<img src="images/frequency_reading_push.png" style="width: 200px; height:360px"/>

We recommend sending data in intervals and avoiding [Flood Error](http://docs.blynk.cc/#troubleshooting-flood-error).
For example, this [SimpleTimer Library](http://playground.arduino.cc/Code/SimpleTimer) is an Arduino library for timed events. 
Please read instructions inside this [example sketch](https://github.com/blynkkk/blynk-library/blob/master/examples/GettingStarted/PushData/PushData.ino#L30) for more details.

SimpleTimer is included in Blynk's library. Here is how it can work:

```cpp
#include <SPI.h>
#include <Ethernet.h>
#include <BlynkSimpleEthernet.h>
#include <SimpleTimer.h> // here is the SimpleTimer library

char auth[] = "YourAuthToken"; // Put your token here

SimpleTimer timer; // Create a Timer object called "timer"! 

void setup()
{
  Serial.begin(9600);
  Blynk.begin(auth);
  
  timer.setInterval(1000L, sendUptime); //  Here you set interval (1sec) and which function to call 
}

void sendUptime()
{
  // This function sends Arduino up time every 1 second to Virtual Pin (V5)
  // In the app, Widget's reading frequency should be set to PUSH
  // You can send anything with any interval using this construction
  // Don't send more that 10 values per second
  
  Blynk.virtualWrite(V5, millis() / 1000);
}

void loop()
{
  Blynk.run(); // all the Blynk magic happens here
  timer.run(); // SimpleTimer is working
}
```

**Sketch:** [PushData](https://github.com/blynkkk/blynk-library/blob/master/examples/GettingStarted/PushData/PushData.ino#L30)

##State syncing

###For hardware
If your hardware looses Internet connection or resets, you can restore all the values from Widgets in the Blynk app.

```cpp
BLYNK_CONNECTED() {
  if (isFirstConnect) {
    Blynk.syncAll();
  }
}

//here handlers for sync command
BLYNK_WRITE(V0) {
   ....
}

```

The ```Blynk.syncAll()``` command restores all the Widget's values based on the last saved values on the server. 
All analog and digital pin states will be restored. Every Virtual Pin will perform ```BLYNK_WRITE``` event.

[Sync Hardware with App state](https://github.com/blynkkk/blynk-library/blob/master/examples/More/Sync/HardwareSyncStateFromApp/HardwareSyncStateFromApp.ino)

You can also update a single Virtual Pin value by calling ```Blynk.syncVirtual(V0)``` or you can update several pins with 
```Blynk.syncVirtual(V0, V1, V2, ...)```.

You can also use server to store any value without widget. Just call ```Blynk.virtualWrite(V0, value)```.

[Storing single value on server](https://github.com/blynkkk/blynk-library/blob/master/examples/More/ServerAsDataStorage/ServerAsDataStorage_SingleValue/ServerAsDataStorage_SingleValue.ino)

[Storing multiple values on server](https://github.com/blynkkk/blynk-library/blob/master/examples/More/ServerAsDataStorage/ServerAsDataStorage_MultiValue/ServerAsDataStorage_MultiValue.ino)

###For app
If you need to keep your hardware in sync with Widgets' state even if app is offline use ```Blynk.virtualWrite```.

Imagine you have a LED Widget connected to the Virtual Pin V1 in the app, and a physical button attached to your hardware. 
When you press a physical button, you would expect to see updated state of the LED Widget in the app. 
To achieve that you need to send ```Blynk.virtualWrite(V1, 255)``` when a physical button gets pressed.

[Represent physical button state via LED widget with interrupts](https://github.com/blynkkk/blynk-library/blob/master/examples/More/Sync/ButtonInterrupt/ButtonInterrupt.ino)

[Represent physical button state via LED widget with polling](https://github.com/blynkkk/blynk-library/blob/master/examples/More/Sync/ButtonPoll/ButtonPoll.ino)

[Represent physical button state via Button widget with polling](https://github.com/blynkkk/blynk-library/blob/master/examples/More/Sync/SyncPhysicalButton/SyncPhysicalButton.ino)

## Control of multiple devices
Latest Blynk Android app version has support of multiple devices. That means you can assign any widget to specific device with own 
auth token. 
For example - you may have button on V1 that controls wi-fi bulb A and another button on V1 that controls wi-fi bulb B. In order 
to do this you need more than 1 device within your project. To achieve this please go to project settings and click on "Devices" section : 

<img src="images/new_project_settings.png" style="width: 200px; height:360px"/>

You'll see list of devices :
 
<img src="images/list_of_devices.png" style="width: 200px; height:360px"/>

So you can add new device : 

<img src="images/new_device.png" style="width: 200px; height:360px"/>

After above steps, every widget will have one more field "Target" : 

<img src="images/widget_settings_devices.png" style="width: 200px; height:360px"/>

Now you need to assign widget to device and after that widget will control only this specific device.

That's it! Now you need to upload sketches with correct Auth Tokens to your hardware.

## Devices online status
Latest Blynk Android app version has support for online statuses for multiple devices.
 
<img src="images/online_status.png" style="width: 200px; height:360px"/>

In ideal world when device closes tcp connection with some ```connection.close()``` - connected server will get notification 
regarding closed connection. So you can get instant status update on UI. However in real world this mostly exceptional situation. 
In majority of cases there is no easy and instant way to find out that connection is not active anymore. 

That's why Blynk uses ```HEARTBEAT``` mechanism. With this approach hardware periodically sends ```ping``` command with predefined 
interval (10 seconds by default, ```BLYNK_HEARTBEAT``` [property](https://github.com/blynkkk/blynk-library/blob/master/src/Blynk/BlynkConfig.h)). 
In case hardware don't send anything within 10 seconds server waits additional 5 seconds and after that connection 
assumed to be broken and closed by server. So on UI you'll see connection status update only after 15 seconds when it is 
actually happened.

You can also change ```HEARTBEAT``` interval from hardware side via ```Blynk.config```. In that case 
```newHeartbeatInterval * 2.3``` formula will be applied. So in case you you decided to set ```HEARTBEAT``` interval to 
5 seconds. You'll get notification regarding connection with 11 sec delay in worst case.

## Change Widget properties
Latest Blynk library supports changing some of the widget properties from hardware side. 
For example, you can change the color of LED widget based on a condition. For example :

```
//change LED color
Blynk.setProperty(V0, "color", "#D3435C");

//change LED label
Blynk.setProperty(V0, "label", "My New Widget Label");

//change MENU labels
Blynk.setProperty(V0, "labels", "Menu Item 1", "Menu Item 2", "Menu Item 3");

```

[Set Property for single value field](https://github.com/blynkkk/blynk-library/blob/master/examples/More/SetProperty/SetProperty_SingleValue/SetProperty_SingleValue.ino)

[Set Property for multi value field](https://github.com/blynkkk/blynk-library/blob/master/examples/More/SetProperty/SetProperty_MultiValue/SetProperty_MultiValue.ino)

**NOTE : ** Changing these parameters work **only** for widgets attached to Virtual pins.

Two widget properties are supported - ```color```, ```label``` for all widgets : 

```label``` is string for label of all widgets.

```color``` is string in [HEX](http://www.w3schools.com/html/html_colors.asp) format (in the form: #RRGGBB, 
where RR (red), GG (green) and BB (blue) are hexadecimal values between 00 and FF). For example :
``` 
#define BLYNK_GREEN     "#23C48E"
#define BLYNK_BLUE      "#04C0F8"
#define BLYNK_YELLOW    "#ED9D00"
#define BLYNK_RED       "#D3435C"
#define BLYNK_DARK_BLUE "#5F7CD8"
``` 

Widget specific properties: 

**Button**

```onLabel``` is string for ON label of button;

```offLabel``` is string for OFF label of button;

**Music Player**

```isOnPlay``` is boolean accepts true/false.
``` 
Blynk.setProperty(V0, "isOnPlay", "true");
``` 

**Menu**

```labels``` is list of strings for Menu widget selections;
``` 
Blynk.setProperty(V0, "labels", "label 1", "label 2", "label 3");
``` 

You can also change widget properties via [HTTP API](http://docs.blynkapi.apiary.io/#).

##Limitations and Recommendations
- Don't put ```Blynk.virtualWrite``` and any other ```Blynk.*``` command inside ```void loop()```- it will cause 
lot's of outgoing messages to our server and your connection will be terminated; 

- We recommend calling functions with intervals. For example, this 
[SimpleTimer Library](http://playground.arduino.cc/Code/SimpleTimer) is a simple library for timed events. 
Please read instructions inside this [example sketch](https://github.com/blynkkk/blynk-library/blob/master/examples/GettingStarted/PushData/PushData.ino#L30) for more details;

- Avoid using long delays with ```delay()``` – it may cause connection breaks;

- If you send more than 100 values per second - you may cause 
[Flood Error](http://docs.blynk.cc/#troubleshooting-flood-error) and your hardware will be automatically disconnected from the server;

- Be careful sending a lot of ```Blynk.virtualWrite``` commands as most hardware is not very powerful (like ESP8266) 
so it may not handle many requests. 
