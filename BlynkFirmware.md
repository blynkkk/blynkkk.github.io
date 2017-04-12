#Blynk Firmware
## Configuration

### Blynk.begin()

The simplest way to configure Blynk is to call ```Blynk.begin()```:

```cpp
Blynk.begin(auth, ...);
```
It has various parameters for different hardware, depending on the type of connection you use. Follow the example sketches for your board.

```begin()``` is basically doing these steps:

1. Connects to network (WiFi, Ethernet, ...)
2. Calls ```Blynk.config(...)``` - sets auth token, server address
3. Tries to connects to the server once (can block for more than 30s)

### Blynk.config()

```config()``` allows you to manage network connection yourself.
You can set up your shield (WiFi, Ethernet, ...) manually, and then call:

```cpp
Blynk.config(auth, server, port);
```
or just
```cpp
Blynk.config(auth);
```

**Note:** Just after ``` Blynk.config(...) ```, Blynk is not yet connected to the server.  
It will try to connect when it reaches first ``` Blynk.run() ``` or ``` Blynk.connect() ```call.  
If you want to skip connecting to the server, just call ``` Blynk.disconnect() ``` right after configuration.

For setting-up WiFi connection, you can use a ```connectWiFi``` (just for convenience):

```cpp
Blynk.connectWiFi(ssid, pass);
```
To connect to open WiFi networks, set pass to an empty string (```""```).

## Connection management

There are several functions to help with connection management:

### Blynk.connect()

```cpp
# This functions will try connecting to Blynk server.
# Returns true when connected, false if timeout reached.
# Default timeout is 30 seconds.
bool result = Blynk.connect();
bool result = Blynk.connect(timeout);
```

### Blynk.disconnect()

To disconnect from Blynk server, use:

```cpp
Blynk.disconnect();
```

### Blynk.connected()
To get the status of connection to Blynk Server use:

```cpp
bool result = Blynk.connected();
```

If your shield/connection type is not supported yet - you can craft it yourself easily! 
[Here is an example](https://github.com/blynkkk/blynk-library/blob/master/examples/Boards_USB_Serial/User_Defined_Connection/User_Defined_Connection.ino).

### Blynk.run()
This function should be called frequently to process incoming commands and perform housekeeping of Blynk connection.
It is usually called in ``` void loop() {} ```.

You can initiate it in other places, unless you run out of heap memory (in the cascaded functions with local memory).
For example, it is not recommended to call ``` Blynk.run() ``` inside of the  ```BLYNK_READ ``` and ``` BLYNK_WRITE ``` functions on low-RAM devices.

## Digital & Analog pins control
The library can perform basic pin IO (input-output) operations out-of-the-box:

    digitalRead
    digitalWrite
    analogRead
    analogWrite (PWM or Analog signal depending on the platform)

No need to write code for simple things like LED, Relay control and analog sensors.

## Virtual pins control
Virtual Pins are designed to send any data from your microcontroller to the Blynk App and back. 
Think about Virtual Pins as channels for sending any data. Make sure you differentiate Virtual Pins from physical 
pins on your hardware. Virtual Pins have no physical representation.

Virtual Pins can be used to interface with libraries (Servo, LCD and others) and implement custom functionality. 
The device may send data to the App using  ```Blynk.virtualWrite(pin, value)``` and receive data from the App using ```BLYNK_WRITE(vPIN)```.

#### Virtual Pin data types
The actual values are sent as strings, so there are no practical limits on the data that can be sent.  
However, remember the limitations of the platform when dealing with numbers. For example the integer on Arduino 
is 16-bit, allowing range -32768 to 32767.
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

### Blynk.virtualWrite(vPin, value)

You can send all the formats of data to Virtual Pins

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

**Note:** Calling ```virtualWrite``` attempts to send the value to the network immediately.

### Blynk.setProperty(vPin, "property", value)

This allows [changing widget properties](#blynk-main-operations-change-widget-properties)

### BLYNK_WRITE(vPIN)

```BLYNK_WRITE``` defines a function that is called when device receives an update of Virtual Pin value from the server:

```cpp
BLYNK_WRITE(V0)
{   
  int value = param.asInt(); // Get value as integer
  
  // The param can contain multiple values, in such case:
  int x = param[0].asInt();
  int y = param[1].asInt();
}
```

### BLYNK_READ(vPIN)

```BLYNK_READ``` defines a function that is called when device is requested to send it's current value of Virtual Pin to the server. Normally, this function should contain some ```Blynk.virtualWrite``` calls.

```cpp
BLYNK_READ(V0)
{
  Blynk.virtualWrite(V0, newValue);
}
```

### BLYNK_WRITE_DEFAULT()

This redefines the handler for all pins that are not covered by custom ```BLYNK_WRITE``` functions.

```cpp
BLYNK_WRITE_DEFAULT()
{
  int pin = request.pin;      // Which exactly pin is handled?
  int value = param.asInt();  // Use param as usual.
}
```

### BLYNK_READ_DEFAULT()

This redefines the handler for all pins that are not covered by custom ```BLYNK_READ``` functions.

```cpp
BLYNK_READ_DEFAULT()
{
  int pin = request.pin;      // Which exactly pin is handled?
  Blynk.virtualWrite(pin, newValue);
}
```

### BLYNK_CONNECTED()

This function is called every time Blynk gets connected to the server. It's convenient to call sync functions here.

```cpp
BLYNK_CONNECTED() {
// Your code here
}
```

### Blynk.syncAll()

Request server to send the most recent values for all widgets. In other words, all analog/digital pin states will be restored and every virtual pin will generate BLYNK_WRITE event.

```cpp
BLYNK_CONNECTED() {
  if (isFirstConnect) {
    Blynk.syncAll();
  }
}
```

### Blynk.syncVirtual(vPin)

Requests virtual pins value update. The corresponding ```BLYNK_WRITE``` handler is called as the result.

```cpp
Blynk.syncVirtual(V0);
# Requesting multiple pins is also supported:
Blynk.syncVirtual(V0, V1, V6, V9, V16);
```

## BlynkTimer

```BlynkTimer``` enables you to perform periodic actions in the main ```loop()``` context.  
It is the same as widely used SimpleTimer, but fixes several issues and is included in Blynk library by default.  
**Please note that a single BlynkTimer object allows to schedule up to 16 timers.**

For more information on timer usage, please see: http://playground.arduino.cc/Code/SimpleTimer

## Debugging

### #define BLYNK_PRINT
### #define BLYNK_DEBUG

To enable debug prints on the default Serial, add on the top of your sketch **(should be the first line)**:

```cpp
#define BLYNK_PRINT Serial // Defines the object that is used for printing
#define BLYNK_DEBUG        // Optional, this enables more detailed prints
```

And enable Serial Output in setup():

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

## Minimizing footprint

To minimize the program Flash/RAM, you can disable some of the built-in functionality:

1. Comment-out ```#define BLYNK_PRINT``` to remove prints
2. Put on the top of your sketch:
```
#define BLYNK_NO_BUILTIN   // Disable built-in analog & digital pin operations
#define BLYNK_NO_FLOAT     // Disable float operations
```

## Porting, hacking

If you want to dive into crafting/hacking/porting Blynk library implementation, please also check [this documemtation](https://github.com/blynkkk/blynk-library/tree/master/extras/docs).
