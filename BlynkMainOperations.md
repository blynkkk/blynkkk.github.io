#Blynk main operations

##Virtual Pins
Blynk can control Digital and Analog IO Pins on you hardware directly. You don't even need to write code for it. 
It's great for blinking LEDs, but often it's just not enough...

We designed Virtual Pins to send **any** data from your microcontroller to the Blynk App and back. 

It opens huge opportunities for you, because anything you plug in to your hardware will be able to talk to Blynk.
With Virtual Pins you can send something from the App, process it on Arduino and then send it back to the smartphone 
based on any logic you want. You can trigger functions, read I2C devices, convert values, control any servo motor and so on.

Virtual Pins can be used to interface with external libraries (Servo, LCD and others) and implement custom functionality. 
The device may send data to the Widgets to the Virtual Pin like this:

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
When you press Button, Blynk App sends ```1``` On second click - it sends ```0``` 

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
Just set the frequency to PUSH mode

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
Blynk allows you easily restore hardware state from widget values in case your hardware was reset or disconnected. 
We call this feature state syncing. Here is simple code snippet:

```cpp
BLYNK_CONNECTED() {
  if (isFirstConnect) {
    Blynk.syncAll();
  }
}
```

The ```Blynk.syncAll()``` command set all widget values based on the last state, stored on the server. In other words, all analog/digital pin states will be restored and every virtual pin will generate BLYNK_WRITE event.

[Full Sketch](https://github.com/blynkkk/blynk-library/blob/master/examples/More/Sync/Sync.ino)

You can also request a single virtual pin value update by calling ```Blynk.syncVirtual(pin)```. The corresponging BLYNK_WRITE will be called with the new value.

###For app
In real world your Blynk application will be turned off for a long periods while in pocket. But in case you still need 
to hold your hardware in sync with widgets state even app is offline - you need to call ```Blynk.virtualWrite```.
Let's assume you have a switch button on virtual pin 1 in app and physical button on hardware. You turn off your app. Press a physical
button and expect to see button turned on when your app goes online. So in order to make this assumption true you need
to send ```Blynk.virtualWrite(V1, HIGH)``` on physical button press.

//todo add sketch example.

##Limitations and Recommendations
- Don't put ```Blynk.virtualWrite``` and any other ```Blynk.*``` command inside ```void loop()```- it will cause 
lot's of outgoing messages to our server and your connection will be terminated; 

- We recommend calling functions with intervals. For example, this 
[SimpleTimer Library](http://playground.arduino.cc/Code/SimpleTimer) is a simple library for timed events. 
Please read instructions inside this [example sketch](https://github.com/blynkkk/blynk-library/blob/master/examples/GettingStarted/PushData/PushData.ino#L30) for more details;

- Avoid using long delays with ```delay()``` – it may cause connection breaks;

- If you send more than 10-100 (depends on hardware) values per second - you'll cause 
[Flood Error](http://docs.blynk.cc/#troubleshooting-flood-error)* and connection to your hardware will be terminated;
