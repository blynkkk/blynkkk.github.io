#Blynk Firmware
## Configuration

### Blynk.begin()

The easiest way to configure Blynk is to use ```Blynk.begin()```:

```cpp
Blynk.begin(auth, ...);
```
It has multiple parameters for different hardware models and it also depends on the type of connection. Follow the example sketches for your specific hardware model.

What happens inside of ```Blynk.begin()``` function:

1. Connection to the network (WiFi, Ethernet, ...)
2. Call of ```Blynk.config(...)``` to set Auth Token, Server Address, etc.
3. Attempts to connect to the server once (can block for more than 30s)

If your shield/connection type is not supported yet - you can implement it by yourself. [Here are some examples](https://github.com/blynkkk/blynk-library/tree/master/examples/More/ArduinoClient).

### Blynk.config()

```config()``` allows you to manage network connection. You can set up your connection type (WiFi, Ethernet, ...) by yourself, and then call:

```cpp
Blynk.config(auth, server, port);
```
or just
```cpp
Blynk.config(auth);
```

**NOTE: After ``` Blynk.config(...) ``` is called, your hardware is not yet connected to the server.** 
It will try to connect while until it hits first instance of ``` Blynk.run() ``` or ``` Blynk.connect() ```routine.  
To skip connecting to the server or to disconnect manually, call ``` Blynk.disconnect() ``` after configuration.

Use ```connectWiFi``` to conveniently set up WiFi connection:

```cpp
Blynk.connectWiFi(ssid, pass);
```
To connect to open WiFi networks, set pass to an empty string (```""```).

## Connection management

There are several functions to help with connection management:

### Blynk.connect()

This functions will continue trying to connect to Blynk server. 
Returns `true` when connected, `false` if timeout have been reached.
Default timeout is 30 seconds.

```cpp
bool result = Blynk.connect();
bool result = Blynk.connect(timeout);
```

### Blynk.disconnect()

Disconnects hardware from Blynk server:

```cpp
Blynk.disconnect();
```

### Blynk.connected()
Returns `true` when hardware is connected to Blynk Server, `false` if there is no active connection to Blynk server.

```cpp
bool result = Blynk.connected();
```

### Blynk.run()
This function should be called frequently to process incoming commands and perform housekeeping of Blynk connection.
It is usually called in ``` void loop() {} ```.

This command can be initiated it in other places of your code unless you run out of heap memory (in the cascaded functions with local memory).

For example, it is not recommended to call ``` Blynk.run() ``` inside of the  ```BLYNK_READ ``` and ``` BLYNK_WRITE ``` functions on low-RAM devices.

## Digital & Analog pins control
Blynk library can perform basic pin IO (input-output) operations out-of-the-box:

    digitalRead
    digitalWrite
    analogRead
    analogWrite (PWM or Analog signal depending on the platform)

No need to write code for simple things like LED, Relay control and analog sensors. Just choose a corresponding Pin in Blynk app and control it directly with no additional code

## Virtual pins control
Virtual Pins is a way to exchange any data between your hardware and Blynk app. 
Think about Virtual Pins as channels for sending any data. Make sure you differentiate Virtual Pins from physical GPIO
pins on your hardware. Virtual Pins have no physical representation.

Virtual Pins are commonly used to interface with other libraries (Servo, LCD and others) and implement custom logic. 
The device can send data to the App using  ```Blynk.virtualWrite(pin, value)``` and receive data from the App using ```BLYNK_WRITE(vPIN)```. Read below

#### Virtual Pin data types
All Virtual Pin values are always sent as Strings and there are no practical limits on the data that can be sent.  
However, there are certian limitations on the hardware side when dealing with numbers. For example, the integer on Arduino 
is 16-bit, allowing range -32768 to 32767.

To interpret incoming data as Integers, Floats, Doubles and Strings use:

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

### Blynk.virtualWrite(vPin, value)

**NOTE: Use BlynkTimer when you use this command to send data. Otherwise your hardware will be disconnected from the server**

Send data in various formats to Virtual Pins.

```cpp
// Send string
Blynk.virtualWrite(pin, "abc");

// Send integer
Blynk.virtualWrite(pin, 123);

// Send float
Blynk.virtualWrite(pin, 12.34);

// Send multiple values as an array
Blynk.virtualWrite(pin, "hello", 123, 12.34);

// Send RAW data
Blynk.virtualWriteBinary(pin, buffer, length);
```

Calling ```virtualWrite``` attempts to send the value to the network immediately.

## BlynkTimer
It's important to send data in intervals and keep the void loop() as clean as possible. 

`BlynkTimer` allows you to send data periodically with given intervals not interfering with Blynk library routines 
`Blynk Timer` inherits [SimpleTimer Library](http://playground.arduino.cc/Code/SimpleTimer), a well known and widely used library to time multiple events on hardware.
`BlynkTimer` is included in Blynk library by default and there is no need to install SimpleTimer separately or include `SimpleTimer.h`   

- A single `BlynkTimer` object allows to schedule up to 16 timers
- Improved compatibility with boards like `Arduino 101`, `Intel Galileo`, etc.
- When a timer struggles to run multiple times (due to a blocked `loop`), it just skips all the missed intervals, and calls your function only once. This differs from `SimpleTimer`, which could call your function multiple times in this scenario.

For more information on timer usage, please see: http://playground.arduino.cc/Code/SimpleTimer  
And here is a BlynkTimer [example sketch](https://github.com/blynkkk/blynk-library/blob/master/examples/GettingStarted/PushData/PushData.ino#L30).

Please also remember that a single ```BlynkTimer``` can schedule many timers, so most probably you need only one instance of BlynkTimer in your sketch.


### BLYNK_WRITE(vPIN)

```BLYNK_WRITE``` is a function called every time device gets an update of Virtual Pin value from the server (or app):

To read the received data use:

```cpp
BLYNK_WRITE(V0)
{   
  int value = param.asInt(); // Get value as integer
  
  // The param can contain multiple values, in such case:
  int x = param[0].asInt();
  int y = param[1].asInt();
}
```

**`BLYNK_WRITE` can't be used inside of any loop or function. It's a standalone function.**


### BLYNK_READ(vPIN)

```BLYNK_READ``` is function called when device is requested to send it's current value of Virtual Pin to the server. Normally, this function should contain ```Blynk.virtualWrite``` call(s).

```cpp
BLYNK_READ(V0)
{
  Blynk.virtualWrite(V0, newValue);
}
```

### BLYNK_WRITE_DEFAULT()

Redefines the handler for all pins that are not covered by custom ```BLYNK_WRITE``` functions.

```cpp
BLYNK_WRITE_DEFAULT()
{
  int pin = request.pin;      // Which exactly pin is handled?
  int value = param.asInt();  // Use param as usual.
}
```

### BLYNK_READ_DEFAULT()

Redefines the handler for all pins that are not covered by custom ```BLYNK_READ``` functions.

```cpp
BLYNK_READ_DEFAULT()
{
  int pin = request.pin;      // Which exactly pin is handled?
  Blynk.virtualWrite(pin, newValue);
}
```

### BLYNK_CONNECTED()

Use this function when you need to run certain routine when hardware connects to Blynk Cloud or private server. It's common to call sync functions inside of this function.

```cpp
BLYNK_CONNECTED() {
// Your code here
}
```

### BLYNK_APP_CONNECTED()

This function is called every time Blynk app client connects to Blynk server.

```cpp
BLYNK_APP_CONNECTED() {
// Your code goes here
}
```

**Note: Ennable this feature in Project Settings first:**

<img src="images/app_connected_setting.png" style="width: 200px; height:360px"/>

[Example](https://github.com/blynkkk/blynk-library/blob/master/examples/More/AppConnectedEvents/AppConnectedEvents.ino)

### BLYNK_APP_DISCONNECTED()

This function is called every time the Blynk app disconnects from Blynk Cloud or private server.

```cpp
BLYNK_APP_DISCONNECTED() {
// Your code here
}
```

**Note: Enable this feature in Project Settings first:**

<img src="images/app_connected_setting.png" style="width: 200px; height:360px"/>

[Example](https://github.com/blynkkk/blynk-library/blob/master/examples/More/AppConnectedEvents/AppConnectedEvents.ino)

### Blynk.syncAll()

Requests all stored on the server latest values for all widgets. All analog/digital/virtual pin values and states will be set to the latest stored value. Every virtual pin will generate BLYNK_WRITE() event.

```cpp
BLYNK_CONNECTED() {
    Blynk.syncAll();
}
```

### Blynk.syncVirtual(vPin)

This command updates individual Virtual Pin to the latest stored value on the server. When it's used, a corresponding ```BLYNK_WRITE``` handler is called.

```cpp
Blynk.syncVirtual(V0);
```

To update multiple pins, use:

```
Blynk.syncVirtual(V0, V1, V6, V9, V16);
```

### Blynk.setProperty(vPin, "property", value)

This command allows [changing widget properties](#blynk-main-operations-change-widget-properties)


## Debugging

### #define BLYNK_PRINT
### #define BLYNK_DEBUG

To enable debug prints on the default Serial port add on the top of your sketch 
**IMPORTANT: This should be the first line in your code**:

```cpp
#define BLYNK_PRINT Serial // Defines the object that is used for printing
#define BLYNK_DEBUG        // Optional, this enables more detailed prints
```

Then enable Serial Output in setup():

```cpp
Serial.begin(9600);
```
Open Serial Monitor and you'll see the debug prints.

You can also use spare Hardware serial ports or SoftwareSerial for debug output (you will need an adapter to connect to it with your PC).

<span style="color:#D3435C;">**WARNING:** Enabling ```BLYNK_DEBUG``` will slowdown your hardware processing speed up to 10 times!</span>

### BLYNK_LOG()

When ```BLYNK_PRINT``` is defined, you can use ```BLYNK_LOG``` to print your logs. The usage is similar to ```printf```:

```cpp
BLYNK_LOG("This is my value: %d", 10);
```

On some platforms (like Arduino 101) the ```BLYNK_LOG``` may be unavailable, or may just use too much resources.  
In this case you can use a set of simpler log functions:

```cpp
BLYNK_LOG1("Hello World"); // Print a string
BLYNK_LOG1(10);      // Print a number
BLYNK_LOG2("This is my value: ", 10); // Print 2 values
BLYNK_LOG4("Temperature: ", 24, " Humidity: ", 55); // Print 4 values
...
```

## Minimizing footprint

To minimize the program Flash/RAM, you can disable some of the built-in functionality:

1. Comment-out ```#define BLYNK_PRINT``` to remove prints
2. Put on the top of your sketch:
```
#define BLYNK_NO_BUILTIN   // Disable built-in analog & digital pin operations
#define BLYNK_NO_FLOAT     // Disable float operations
```

## Porting, hacking

If you want to dive into crafting/hacking/porting Blynk library implementation, please also check [this documentation](https://github.com/blynkkk/blynk-library/tree/master/extras/docs).
