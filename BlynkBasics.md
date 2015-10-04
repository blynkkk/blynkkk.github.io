#Blynk Basics

You can find [example sketches](https://github.com/blynkkk/blynk-library/tree/master/examples) covering basic Blynk Features. They are included in the libary. All the sketches are designed to be easily combined with each other.
 
##How it works?
**Blynk works over the Internet.** So the one and only requirement is that your hardware can talk to the Internet.

No matter what type of connection you choose - Ethernet, Wi-Fi or maybe this new ESP8266 everyone is talking about – Blynk libraries and example sketches will get you online, connect to Blynk Server and pair up with your smartphone.
 
<img src="images/architecture.png" style="width: 450px;"/>

It's not that easy to take Arduino out of your home network, so we've built a [Blynk server](https://github.com/blynkkk/blynk-server). It handles all the authentication and communication, and also keeps an eye on your board while the smartphone is offline. Blynk server runs on Java and is open-source. You will be able to run it locally if you really need to. Messaging between mobile apps , Blynk Server and Arduino is based on a simple, lightweight and fast binary protocol over TCP/IP sockets.
 
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
* Device-to-Device communication using Bridge Widget
* Sending emails, tweets, push notifications, etc.
* ... more features are constantly added!

### Configuration

The simplest way to configure Blynk is to call Blynk.begin():
```cpp
Blynk.begin(auth, ...);
```
begin() can have different parameters for different boards, so follow the example for your board/type of connection.

A more advanced way is to setup the shield (WiFi, Ethernet) manually, and then call ``` blynk.config(...)```:

```cpp
Blynk.config(auth);
```
```cpp
Blynk.config(auth, server, port);
```

For WiFi connections, you can use a ``` connectWiFi ``` (just for convenience).
```cpp
Blynk.connectWiFi(ssid, pass)
```
To connect to Open WiFi networks, set pass to an empty string ("").

### Connection management

There are several functions to help with connection management:
```cpp
# This will try connecting to Blynk server. Default timeout is 30 seconds
bool result = Blynk.connect();
bool result = Blynk.connect(timeout);
```
```cpp
# This will disconnect from Blynk server
Blynk.disconnect();
```
```cpp
# This returns if we're currently connected
bool result = Blynk.connected();
```
**Note:** Just after ``` Blynk.begin(...) ``` or ``` Blynk.config(...) ```, Blynk is not yet connected to the server.
It will try to connect when it hits first ``` Blynk.run() ``` or ``` Blynk.connect() ``` call.

If you want to skip connecting to the server, just call ``` disconnect() ``` right after configuration.

If your shield/connection type is not supported yet - you can craft it yourself easily! [Here is an example](https://github.com/blynkkk/blynk-library/blob/master/examples/BoardsAndShields/User_Defined_Connection/User_Defined_Connection.ino).

### Blynk.run()
This function should be called frequently to process incoming commands and perform housekeeping of Blynk connection.
It is usually called in ``` void loop() {} ```.
You can call it in other places, unless you run out of heap memory (in the cascaded functions with local memory).
For example, it is not recommended to call ``` Blynk.run() ``` inside of the  ```BLYNK_READ ``` and ``` BLYNK_WRITE ``` functions on low-RAM devices.

### Digital & Analog pins

The library can perform basic pin IO (input-output) operations out-of-the-box:

    digitalRead
    digitalWrite
    analogRead
    analogWrite (PWM or Analog signal depending on the platform)

So, there is no need to write code for simple things like LED, Relay control, and analog sensors.

##Virtual Pins
Virtual Pins are designed to send any data from your microcontroller to the Blynk App and back. Think about Virtual Pins as channels for sending any data. Make sure you differentiate Virtual Pins from physical pins on your hardware. Virtual Pins have no physical representation.

Virtual Pins can be used to interface with libraries (Servo, LCD and others) and implement custom functionality. The device may send data to the Widget to the Virtual Pin like this:
```cpp
Blynk.virtualWrite(pin, "abc");
Blynk.virtualWrite(pin, 123);
Blynk.virtualWrite(pin, 12.34);
```

###Sending data to hardware
All [Controller Widgets](http://blynkkk.github.io/#widgets-controllers) can send data to Virtual Pins on your hardware. For instance, below code shows how to retrieve 1 and 0 int value on hardware via pressing button on virtual pin 1 within Application:
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

###Data types
The actual values are sent as strings, so there is no practical limits on the data that can be sent.  
However, remember the limitations of the platform when dealing with numbers. For example the integer on Arduino is 16-bit, allowing range -32768 to 32767.
You can interpret incoming data as Integers, Floats, Doubles and Strings:
```cpp
param.asInt();
param.asFloat();
param.asDouble();
param.asStr();
```

You can also get the RAW data from the param buffer:

```cpp
param.getBuffer()
param.getLength()
```

###Limitations and recommendations

- Don't put ```Blynk.virtualWrite``` and any other ```Blynk.*``` command inside ```void loop()```. This will cause lot's of outgoing messages to our server and your connection will be terminated. We suggest you to use [SimpleTimer](http://playground.arduino.cc/Code/SimpleTimer) library for events that are executed in intervals. Read instructions inside this [sketch](https://github.com/blynkkk/blynk-library/blob/master/examples/GettingStarted/PushData/PushData.ino#L30) for more details.
- Avoid using long delays with ```delay()``` – it may cause connection breaks
- Don't send more that 10 values per second - otherwise you'll get FLOOD error and your connection will be terminated.


##Blynk Commands
The library can perform basic pin IO (input-output) operations out-of-the-box:

```
digitalRead
digitalWrite
analogRead
analogWrite //PWM or Analog signal depending on the platform
```

### BLYNK_WRITE(vPIN)
### BLYNK_READ(vPIN)
### BLYNK_WRITE_DEFAULT()
### BLYNK_READ_DEFAULT()
### Blynk.virtualWrite();

You can send all the formats of data to Virtual Pins

```cpp
Blynk.virtualWrite(pin, "abc");
Blynk.virtualWrite(pin, 123);
Blynk.virtualWrite(pin, 12.34);
```

### #define BLYNK_PRINT
### #define BLYNK_DEBUG
### BLYNK_LOG()
To enable debug prints on the default Serial, add on the top of your sketch **(should be the first line
)**:

```cpp
#define BLYNK_DEBUG // Optional, this enables lots of prints
#define BLYNK_PRINT Serial
```
And enable Serial Output in setup():

```cpp
Serial.begin(9600);
```

You can also use spare Hardware serial ports or SoftwareSerial for debug output (you will need an adapter to connect to it with your PC).


<span style="color:#D3435C;">**WARNING:** Enabling Debug mode will slowdown your hardware processing speed up to 10 times!</span>