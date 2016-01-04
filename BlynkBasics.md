#Blynk Basics

You can find [example sketches](https://github.com/blynkkk/blynk-library/tree/master/examples) covering basic Blynk Features. 
They are included in the library. All the sketches are designed to be easily combined with each other.
 
##How does it work?
**Blynk works over the Internet.** So the one and only requirement is that your hardware can talk to the Internet.

No matter what type of connection you choose - Ethernet, Wi-Fi or maybe this new ESP8266 everyone is talking about – 
Blynk libraries and example sketches will get you online, connect to Blynk Server and pair up with your smartphone.
 
<img src="images/architecture.png" style="width: 450px;"/>

It's not that easy to take Arduino out of your home network, so we've built a [Blynk server](https://github.com/blynkkk/blynk-server). 
It handles all the authentication and communication, and also keeps an eye on your board while the smartphone is offline. 
Blynk server runs on Java and is open-source. You will be able to [run it locally](https://github.com/blynkkk/blynk-server#blynk-server) if you really need to. 
Messaging between mobile apps , Blynk Server and Arduino is based on a simple, lightweight and fast binary protocol over TCP/IP sockets.
 
##Features
* Similar API & UI for all supported hardware & devices
* Connection to the cloud using:
  * Ethernet
  * WiFi
  * Bluetooth LE
  * USB (Serial)
  * ...
* Set of easy-to-use Widgets
* Direct pin manipulation with no code writing
* Easy to integrate and add new functionality using virtual pins
* History data monitoring via History Graph widget
* Device-to-Device communication using Bridge Widget
* Sending emails, tweets, push notifications, etc.
* ... more features are constantly added!




###Sending data to hardware
All [Controller Widgets](http://docs.blynk.cc/#widgets-controllers) can send data to Virtual Pins on your hardware. 
For instance, below code shows how to retrieve 1 and 0 int value on hardware via pressing button on virtual pin 1 
within Application:
```cpp
BLYNK_WRITE(1)
{
  int pinData = param.asInt(); 
}
```

and this widget setup:

<img src="images/button_virtual_1.png" style="width: 300px;"/>

In above example when you press button you'll get 1 and on second click 0 within pinData variable.

**Sketch:** [GetData](https://github.com/blynkkk/blynk-library/blob/master/examples/GettingStarted/GetData/GetData.ino#L24)

###Sending data array to hardware 
Some Widgets (e.g Joystick, zeRGBa) have more than one output. 

<img src="images/joystick_merge_mode.png" style="width: 300px;"/>

This output is an array of values. You can get any parameter of the array [0,1,2...] by using: 

```cpp
BLYNK_WRITE(pinNumber)
{   
  int x = param[0].asInt();
  int y = param[1].asInt();
}
```

 **Sketch:** [JoystickTwoAxis](https://github.com/blynkkk/blynk-library/blob/master/examples/Widgets/JoystickTwoAxis/JoystickTwoAxis.ino#L24)

###Sending data to smartphone

There are two ways of pushing data from your hardware to the Widgets in the app over Virtual Pins :

- Using Blynk built-in reading frequency while app active by setting Reading Frequency parameter to required interval:

<img src="images/frequency_reading_pull.png" style="width: 300px;"/>

```cpp
// This function tells Arduino what to do if there is a Widget
// which is requesting data for Virtual Pin (5)
BLYNK_READ(5)
{
  // This command writes Arduino's uptime in seconds to Virtual Pin (5)
  Blynk.virtualWrite(5, millis() / 1000);
}
```

**Sketch:** [PushDataOnRequest](https://github.com/blynkkk/blynk-library/blob/master/examples/GettingStarted/PushDataOnRequest/PushDataOnRequest.ino#L26)

- Writing your own logic of pushing data at any time by setting Reading Frequency parameter to PUSH:

<img src="images/frequency_reading_push.png" style="width: 300px;"/>

```cpp
void sendUptime()
{
  // You can send any value at any time.
  // Please don't send more that 10 values per second.
  Blynk.virtualWrite(5, millis() / 1000);
}
```

**Sketch:** [PushData](https://github.com/blynkkk/blynk-library/blob/master/examples/GettingStarted/PushData/PushData.ino#L30)
