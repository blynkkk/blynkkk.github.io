#Blynk main operations

##Virtual Pins
Virtual Pins are designed to send any data from your microcontroller to the Blynk App and back. Think about Virtual Pins as channels for sending any data. Make sure you differentiate Virtual Pins from physical pins on your hardware. Virtual Pins have no physical representation.

Virtual Pins can be used to interface with libraries (Servo, LCD and others) and implement custom functionality. The device may send data to the Widget to the Virtual Pin like this:

```cpp
Blynk.virtualWrite(pin, "abc");
Blynk.virtualWrite(pin, 123);
Blynk.virtualWrite(pin, 12.34);
```

##Send data from app to hardware
You can send any data from Widgets in the app to your hardware.

All [Controller Widgets](http://blynkkk.github.io/#widgets-controllers) can send data to Virtual Pins on your hardware. For example, code below shows how to get values from the Button Widget in the App

```cpp
BLYNK_WRITE(V1) //Button Widget is writing to pin V1
{
  int pinData = param.asInt(); 
}
```
When you press Button, Blynk App sends ```1``` On second click - it sends ```0``` 

This is how Button Widget is set up:

<img src="images/button_virtual_1.png" style="width: 200px;"/>


Full example sketch: [Get Data](https://github.com/blynkkk/blynk-library/blob/master/examples/GettingStarted/GetData/GetData.ino#L24)

###Sending array from Widget 
Some Widgets (e.g Joystick, zeRGBa) have more than one output. 

<img src="images/joystick_merge_mode.png" style="width: 200px;"/>

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

<img src="images/frequency_reading_pull.png" style="width: 200px;"/>

```cpp
BLYNK_READ(V5) // Widget in the app READs Virtal Pin V5 with the certain frequency
{
  // This command writes Arduino's uptime in seconds to Virtual Pin V5
  Blynk.virtualWrite(5, millis() / 1000);
}
```

**Sketch:** [PushDataOnRequest](https://github.com/blynkkk/blynk-library/blob/master/examples/GettingStarted/PushDataOnRequest/PushDataOnRequest.ino#L26)


###Pushing data from hardware
If you need to PUSH sensor or other data from your hardware to Widget, you can write any logic you want. Just set the frequency to PUSH mode

<img src="images/frequency_reading_push.png" style="width: 200px;"/>

We recommend sending data in intervals and avoiding [Flood Error](http://blynkkk.github.io/#troubleshooting-flood-error).
For example, this [SimpleTimer Library](http://playground.arduino.cc/Code/SimpleTimer) is an Arduino library for timed events. Please read instructions inside this [example sketch](https://github.com/blynkkk/blynk-library/blob/master/examples/GettingStarted/PushData/PushData.ino#L30) for more details.

SimpleTimer is included in Blynk's library. Here is how timed event are handled with it:

```cpp
#include <SPI.h>
#include <Ethernet.h>
#include <BlynkSimpleEthernet.h>
#include <SimpleTimer.h> // here is the SimpleTimer library

char auth[] = "YourAuthToken"; // Put your token here

SimpleTimer timer; // Create a Timer object called...timer! 

void setup()
{
  Serial.begin(9600);
  Blynk.begin(auth);
  
  timer.setInterval(1000L, sendUptime); //  Here you set interval (1sec) and which function to call 
}

void sendUptime()
{
  // This function sends Arduino's up time every 1 second to Virtual Pin (5).
  // In the app, Widget's reading frequency should be set to PUSH. 
  // You can send anything with any interval using this construction
  // Don't send more that 10 values per second.
  
  Blynk.virtualWrite(V5, millis() / 1000);
}

void loop()
{
  Blynk.run(); // all the Blynk magic happens here
  timer.run(); // SimpleTimer is working
}
```

**Sketch:** [PushData](https://github.com/blynkkk/blynk-library/blob/master/examples/GettingStarted/PushData/PushData.ino#L30)

##Data types
The actual values are sent as Strings, so there is no practical limits on the data that can be sent.  
However, remember the limitations of the platform when dealing with numbers. For example, integer values on Arduino are 16-bit, allowing range -32768 to 32767.
You can interpret incoming data as Integers, Floats, Doubles and Strings. Use these commands: 

```cpp
param.asInt(); 		// get an integer value
param.asFloat(); 	// get a float value
param.asDouble();	// get a double value
param.asStr();		// get a string value
```

You can also get the RAW data from the param buffer:

```cpp
param.getBuffer()
param.getLength()
```

##Limitations and Recommendations
- Don't put ```Blynk.virtualWrite``` and any other ```Blynk.*``` command inside ```void loop()```- it will cause lot's of outgoing messages to our server and your connection will be terminated; 

- We recommend calling functions with intervals. For example, this [SimpleTimer Library](http://playground.arduino.cc/Code/SimpleTimer) is a simple library for timed events. Please read instructions inside this [example sketch](https://github.com/blynkkk/blynk-library/blob/master/examples/GettingStarted/PushData/PushData.ino#L30) for more details;

- Avoid using long delays with ```delay()``` – it may cause connection breaks;

- If you send more than 10-100 (depends on hardware) values per second - you'll cause [Flood Error](http://blynkkk.github.io/#troubleshooting-flood-error)* and connection to your hardware will be terminated;
