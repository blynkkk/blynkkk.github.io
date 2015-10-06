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

If your shield/connection type is not supported yet - you can craft it yourself easily! [Here is an example](https://github.com/blynkkk/blynk-library/blob/master/examples/BoardsAndShields/User_Defined_Connection/User_Defined_Connection.ino).

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
##Debugging
### BLYNK_PRINT
TODO:Description how to use

```#define BLYNK_PRINT```

TODO: Output example

### BLYNK_DEBUG
TODO: Description how to use

```#define BLYNK_DEBUG```

TODO: Output example

### BLYNK_LOG()
To enable debug prints on the default Serial, add on the top of your sketch **(should be the first line)**:

```cpp
#define BLYNK_DEBUG // Optional, this enables lots of prints
#define BLYNK_PRINT Serial
```
And enable Serial Output in setup():

```cpp
Serial.begin(9600);
```

Open Serial Monitor and you'll see:
TODO: Output example

You can also use spare Hardware serial ports or SoftwareSerial for debug output (you will need an adapter to connect to it with your PC).

<span style="color:#D3435C;">**WARNING:** Enabling Debug mode will slow down your hardware processing speed up to 10 times!</span>