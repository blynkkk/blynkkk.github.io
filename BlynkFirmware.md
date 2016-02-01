#Blynk Firmware
## Configuration
The simplest way to configure Blynk is to call ```Blynk.begin()```:

```cpp
Blynk.begin(auth, ...);
```
It has various parameters for different hardware, depending on the type of connection you use. Follow the example sketches for your board.

You can also set up shields (WiFi, Ethernet) manually, and then call:

```cpp
Blynk.config(auth);
```
or

```cpp
Blynk.config(auth, server, port);
```

For WiFi connections, you can use a ```connectWiFi``` (just for convenience).

```cpp
Blynk.connectWiFi(ssid, pass)
```
To connect to open WiFi networks, set pass to an empty string ("").

## Connection management
There are several functions to help with connection management:

```cpp
# This functions will keep connecting to Blynk server. Default timeout is 30 seconds
bool result = Blynk.connect();
bool result = Blynk.connect(timeout);
```
To disconnect from Blynk server, use:

```cpp
Blynk.disconnect();
```

To get the status of connection to Blynk Server use:

```cpp
bool result = Blynk.connected();
```

**Note:** Just after ``` Blynk.begin(...) ``` or ``` Blynk.config(...) ```, Blynk is not yet connected to the server.
It will try to connect when it reaches first ``` Blynk.run() ``` or ``` Blynk.connect() ```call.

If you want to skip connecting to the server, just call ``` Blynk.disconnect() ``` right after configuration.

If your shield/connection type is not supported yet - you can craft it yourself easily! 
[Here is an example](https://github.com/blynkkk/blynk-library/blob/master/examples/BoardsAndShields/User_Defined_Connection/User_Defined_Connection.ino).

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

So need to write code for simple things like LED, Relay control and analog sensors.

## Virtual pins control
Virtual Pins are designed to send any data from your microcontroller to the Blynk App and back. 
Think about Virtual Pins as channels for sending any data. Make sure you differentiate Virtual Pins from physical 
pins on your hardware. Virtual Pins have no physical representation.

Virtual Pins can be used to interface with libraries (Servo, LCD and others) and implement custom functionality. 
The device may send data to the App using  ```Blynk.virtualWrite(pin, value)``` and receive data from the App using ```BLYNK_WRITE(vPIN)```.

#### Virtual Pin data types
The actual values are sent as strings, so there is no practical limits on the data that can be sent.  
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

// Send multiple values (up to 4) as an array
Blynk.virtualWrite(pin, "hello", 123, 12.34);

// Send RAW data
Blynk.virtualWriteBinary(pin, buffer, length);
```

**Note:** Calling ```virtualWrite``` attempts to sent the value to the network immediately.

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
  Blynk.virtualWrite(v0, newValue);
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

This redefines the handler for all pins that are not covered by custom ```BLYNK_WRITE``` functions.

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

Requests single virtual pin value update. The corresponding ```BLYNK_WRITE``` handler is called as the result.

```cpp
Blynk.syncVirtual(V0);
```

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

## Porting, hacking

If you want to dive into crafting/hacking/porting Blynk library implementation, please also check [this documemtation](https://github.com/blynkkk/blynk-library/tree/master/docs).
