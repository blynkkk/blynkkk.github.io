#Hardware set ups:
##Arduino over USB (no shield)
If you don't have any shield and your hardware doesn't have any connectivity, you can still use Blynk – directly over USB :

1. Upload [sketch below](https://github.com/blynkkk/blynk-library/blob/master/examples/BoardsAndShields/Arduino_Serial_USB/Arduino_Serial_USB.ino) and change [Auth Token](http://blynkkk.github.io/#getting-started-getting-started-with-application-auth-token)

```cpp
#include <SoftwareSerial.h>
SoftwareSerial SwSerial(2, 3); // RX, TX
#define BLYNK_PRINT SwSerial
#include <BlynkSimpleSerial.h>

// You should get Auth Token in the Blynk App.
// Go to the Project Settings (nut icon).
char auth[] = "YourAuthToken";

void setup()
{
  SwSerial.begin(9600);
  Blynk.begin(auth);
  // Default baud rate is 9600. You could specify it like this:
  //Blynk.begin(auth, 57600);
}

void loop()
{
  Blynk.run();
}
```

2. Run the script in Terminal (script is located in "scripts" folder of library root, 
e.g. 'blynk-library/scripts')
  - for Windows use: ```blynk-ser.bat```
  
  **TODO:** add Windows output
  
  - for Linux and Mac use: ```./blynk-ser.sh``` (may need to run with sudo)

This is what you'll see in Terminal on Mac (usbmodem address can be different):

```
[ Press Ctrl+C to exit ]
/dev/tty.usbmodem not found.
Select serial port [ /dev/tty.usbmodem1451 ]: 
```
Select and copy this serial port address(```/dev/tty.usbmodem1451```) and paste it back:

```
Select serial port [ /dev/tty.usbmodem1451 ]: /dev/tty.usbmodem1451
```

After you press Enter, you should see something similar:

```
Resetting device /dev/tty.usbmodem1451...
Connecting: GOPEN:/dev/tty.usbmodem1451,raw,echo=0,clocal=1,cs8,nonblock=1,ixoff=0,ixon=0,ispeed=9600,ospeed=9600,crtscts=0 <-> openssl-connect:cloud.blynk.cc:8441,cafile=/Users/.../server.crt,nodelay
2015/10/03 00:29:45 socat[30438.2046857984] N opening character device "/dev/tty.usbmodem1451" for reading and writing
2015/10/03 00:29:45 socat[30438.2046857984] N opening connection to LEN=16 AF=2 45.55.195.102:8441
2015/10/03 00:29:45 socat[30438.2046857984] N successfully connected from local address LEN=16 AF=2 192.168.0.2:56821
2015/10/03 00:29:45 socat[30438.2046857984] N SSL connection using AES128-SHA
2015/10/03 00:29:45 socat[30438.2046857984] N starting data transfer loop with FDs [3,3] and [4,4]
```
<span style="color:#D3435C;">**NOTE:** Arduino IDE may complain with "programmer is not responding". You need to terminate script before uploading new sketch.. </span>


##Raspberry Pi
1. Connect your Raspberry Pi to the internet and open it's console.
2. Install WiringPi: http://wiringpi.com/download-and-install/
3. Download and build Blynk:

```bash
$ git clone https://github.com/blynkkk/blynk-library.git
$ cd blynk-library/linux
$ make clean all target=raspberry
```

4. Run Blynk:

```bash
$ sudo ./blynk --token=YourAuthToken
```

5. To enable Blynk auto restart for Pi find */etc/init.d/rc.local* file and add
```
/FULL_PATH_TO_LIB/blynk-library/linux/blynk --token=<Auth Token> 
```
For example:

``` 
/home/pi/blynk-library/linux/blynk --token=<my token> &
```

We have also provided a build script, you can try just running (inside of the "linux" directory):
```bash
$ ./build.sh raspberry
```
Here some additional materials :
- Forum [discussion](http://community.blynk.cc/t/howto-for-raspberry-pi/332);
- Video [tutorial](https://www.youtube.com/watch?v=iSG_8g6KyGE);

##ESP8266 (standalone)

You can run Blynk directly on the ESP8266!

Install the latest ESP8266 for Arduino using [this guide](https://github.com/esp8266/Arduino#installing-with-boards-manager). Also [here](http://www.instructables.com/id/ESP8266-ESP-12Standalone-Blynk-101) and [here russian](http://esp8266.ru/esp8266-blynk) is step-by-step tutorial.

**Sketch:** [ESP8266_Standalone](https://github.com/blynkkk/blynk-library/blob/master/examples/BoardsAndShields/ESP8266_Standalone/ESP8266_Standalone.ino)

##Particle(formely Spark)
Blynk works with the whole family of Particle products: Core, Photon and Electron (soon)

TODO:
>Add screenshots for steps

1. Open [Particle Web IDE](https://build.particle.io/build).
2. Go to the libraries.
3. Search for **Blynk** in the Community Libraries and click on it.
4. Open SparkCore.ino example.
5. Click "use this example".
6. Update your auth token, and upload!


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

All [Controller Widgets](http://blynkkk.github.io/#widgets-controllers) can send data to Virtual Pins on your hardware. For instance, code below shows how to get values from the Button Widget in the App

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

This output is an array of values. You can get any parameter of the array [0,1,2...] by using: 

```cpp
BLYNK_WRITE(V1) // Widget WRITEs to Virtual Pin V1
{   
  int x = param[0].asInt(); // getting first value
  int y = param[1].asInt(); // getting second value
}
```

 **Sketch:** [JoystickTwoAxis](https://github.com/blynkkk/blynk-library/blob/master/examples/Widgets/JoystickTwoAxis/JoystickTwoAxis.ino#L24)

##Get data from hardware
There are two ways of pushing data from your hardware to the Widgets in the app over Virtual Pins :

###Perform requests by Widget
- Using Blynk built-in reading frequency while app is active by setting Reading Frequency parameter to some interval:

<img src="images/frequency_reading_pull.png" style="width: 200px;"/>

```cpp
BLYNK_READ(V5) // Widget in the app READs Virtal Pin V5
{
  // This command writes Arduino's uptime in seconds to Virtual Pin V5
  Blynk.virtualWrite(5, millis() / 1000);
}
```

**Sketch:** [PushDataOnRequest](https://github.com/blynkkk/blynk-library/blob/master/examples/GettingStarted/PushDataOnRequest/PushDataOnRequest.ino#L26)


###Pushing data from hardware
If you need to PUSH sensor or other data from your hardware to Widget in the app you can write any logic you want. Set the widget to PUSH mode

<img src="images/frequency_reading_push.png" style="width: 200px;"/>

We recommend sending data in intervals and avoiiding FLOOD ERROR
For example, this [SimpleTimer Library](http://playground.arduino.cc/Code/SimpleTimer) is an Arduino library for timed events. Please read instructions inside this [example sketch](https://github.com/blynkkk/blynk-library/blob/master/examples/GettingStarted/PushData/PushData.ino#L30) for more details.

```cpp
void sendUptime() // This function should be called based on timer
{
  // You can send any value at any time.
  // Please don't send more that 10 values per second.
  Blynk.virtualWrite(5, millis() / 1000);
}
```

**Sketch:** [PushData](https://github.com/blynkkk/blynk-library/blob/master/examples/GettingStarted/PushData/PushData.ino#L30)

##Data types
The actual values are sent as Strings, so there is no practical limits on the data that can be sent.  
However, remember the limitations of the platform when dealing with numbers. For example, integer values on Arduino are 16-bit, allowing range -32768 to 32767.
You can interpret incoming data as Integers, Floats, Doubles and Strings. Use this commands: 

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
- Don't put ```Blynk.virtualWrite``` and any other ```Blynk.*``` command inside ```void loop()```- it will cause lot's of outgoing messages to our server and your connection will be terminated. 

- We recommend calling functions with intervals. For example, this [SimpleTimer Library](http://playground.arduino.cc/Code/SimpleTimer) is a simple library for timed events. Please read instructions inside this [example sketch](https://github.com/blynkkk/blynk-library/blob/master/examples/GettingStarted/PushData/PushData.ino#L30) for more details.

- Avoid using long delays with ```delay()``` – it may cause connection breaks;

- If you send more than 10 values per second - you'll cause **FLOOD ERROR** and connection to your hardware will be terminated


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


#List Of Supported Hardware

## Platforms

- Arduino (https://github.com/blynkkk/blynk-library)
  - Uno, Duemilanove (select "UNO" in the list, not the "Due")
  - Nano, Mini, Pro Mini, Pro Micro
  - Mega
  - YÚN (onboard WiFi, Ethernet via Bridge)
  - Due - limited support
- Arduino-like
  - ESP8266 (running standalone, using https://github.com/esp8266/Arduino)
  - Wicked WildFire (CC3000)
  - TinyCircuits TinyDuino (CC3000)
  - LightBlue Bean (Bluetooth 4.0 LE). This is only for experts, we're working to simplifying things now...
- Energia
  - RedBearLab (CC3200, WiFi Mini)
- Particle (formerly Spark: https://github.com/vshymanskyy/blynk-library-spark)
  - Core
- LinkIt ONE
- Linux
  - Raspberry Pi
  - PC (Ubuntu, etc)
- Python (scripts only, library on the way!)
  - WiPy
- JavaScript (https://www.npmjs.com/package/blynk-library)
  - Node.js
  - Espruino

## Arduino connection types

- USB (Serial), connected to your laptop or desktop
- Official Ethernet shield (W5100)
- Official Arduino WiFi shield
- Adafruit CC3000 WiFi Breakout / Shield
- ENC28J60 - based boards
- ESP8266 as WiFi modem (running original firmware)
- SeeedStudio Ethernet Shield V2.0 (W5200)
- RN-XV WiFly
- You can implement your own connection type easily (see User_Defined_Connection example)!

## Made by Community

- WIZnet-W5500-EVB (http://instructables.com/id/WIZnet-W5500-EVB-and-Blynk-App-communication)
- TI Tiva C Connected Launchpad (EK-TM4C1294XL1) + Energia 15 (http://community.blynk.cc/t/hardware-supported-by-blynk/16/36)





#Widgets
Widgets are interface modules. Each of them performs a specific input/ output function when communicating with the hardware.

There are 4 types of Widgets: 

- **Controllers** - they send commands to hardware. Use them to control your stuff
- **Displays** - used for various vizualizations of data that comes from hardware to the smartphone
- **Notifications** - are various widgets to send messages and notifications. 
- **Others** - widgets that don't belong to any category

Each Widget has it's own settings. 

Some of the Widgets(e.g. E-mail Widget) are used to enable some functionality and they don't have any settings.
 
## Common Widget Settings
### Pin Selector
This is one of the main parameters you need to set. It defines which pin to control or to read from. 

**Digital Pins** - represent physical Digital IO pins on your hardware. PWM-enabled pins are marked with the ```~``` symbol

**Digital Pins** - represent physical Analog IO pins on your hardware

**Virtual Pins** - have no physical representation. They are used for any data transfer between Blynk App and your hardware.
Read more about Virtual Pins Here.

### Data Mapping
>Screenshot

### SPLIT/MERGE
Some of the Widgets can send more than one value. And with this switch you can control how to send them.
>Screenshot

- SPLIT:
Each of the parameters is sent directly to the Pin on your hardware (e.g D7). You don't need to write any code.

**NOTE:** In this mode you send multiple commands from one widget, which can reduce performance of your hardware.

Example: If you have a Joystick Widget and it's set to D3 and D4, it will send 2 commands over the Internet:

```cpp
digitalWrite(3, value);
digitalWrite(4, value);
```

- MERGE:
When MERGE mode is selected, you are sending just 1 message, consisiting of array of values. But you'll need to parse it on the hardware. 

This mode can be used with Virtual Pins only.

Example: Add a zeRGBa Widget and set it to MERGE mode. Choose Virtual Pin V1

```cpp
BLYNK_WRITE(V1) // There is a Widget that WRITEs data to V1 
{
  int r = param[0].asInt(); // get a RED channel value
  int g = param[1].asInt(); // get a GREEN channel value
  int b = param[1].asInt(); // get a BLUE channel value
}
```


##Controllers
### Button
Works in push or switch modes. Allows to send 0/1 (LOW/HIGH) values.

<img src="images/button.png" style="width: 77px;"/>

<img src="images/button_edit.png" style="width: 200px;"/>

**Sketch:** [BlynkBlink](https://github.com/blynkkk/blynk-library/blob/master/examples/GettingStarted/BlynkBlink/BlynkBlink.ino#L48)

### Slider
Similar to potentiometer. Can be horizontal or vertical. Allows to send values between MIN and MAX.

<img src="images/slider.png" style="width: 77px;"/>

<img src="images/slider_edit.png" style="width: 200px;"/>

**Sketch:** [BlynkBlink](https://github.com/blynkkk/blynk-library/blob/master/examples/GettingStarted/BlynkBlink/BlynkBlink.ino#L48)

### Timer
Timer triggers actions at a specific time. Even if smartphone is offline. Start time sends 1 (HIGH). Stop time sends 0 (LOW).

<img src="images/timer.png" style="width: 77px;"/>

<img src="images/timer_edit.png" style="width: 200px;"/>

**Sketch:** [BlynkBlink](https://github.com/blynkkk/blynk-library/blob/master/examples/GettingStarted/BlynkBlink/BlynkBlink.ino#L48)

### Joystick
Control servo movements in 4 directions

####Settings:
#####SPLIT/MERGE modes
Read Here - Link

#####Rotate on Tilt
When it's ON, Joystck will automatically rotate if you use your smartphone in landscape orientation  
#####Auto-Return
When it's OFF, Joystick handle will not return back to center position. It will stay where you left it. 

<img src="images/joystick.png" style="width: 77px;"/>

<img src="images/joystick_edit.png" style="width: 200px;"/>

**Sketch:** [JoystickTwoAxis](https://github.com/blynkkk/blynk-library/blob/master/examples/Widgets/JoystickTwoAxis/JoystickTwoAxis.ino#L24)

##Displays
### Value Display
Displays incoming data from your sensors or Virtual Pins.

<img src="images/display.png" style="width: 77px;"/> 

<img src="images/display_edit.png" style="width: 200px;"/>

**Sketch:** [BlynkBlink](https://github.com/blynkkk/blynk-library/blob/master/examples/GettingStarted/BlynkBlink/BlynkBlink.ino#L48)

### LED
A simple LED for indication.
TODO: describe 0-255 / 0-1 and fix in apps (make consistent)

<img src="images/led.png" style="width: 77px;"/>

<img src="images/led_edit.png" style="width: 200px;"/>

**Sketch:** [LED](https://github.com/blynkkk/blynk-library/blob/master/examples/Widgets/LED/LED.ino#L31)

### Gauge
A great visual way to display incoming numeric values.

<img src="images/gauge.png" style="width: 77px;"/>

<img src="images/gauge_edit.png" style="width: 200px;"/>

**Sketch:** [BlynkBlink](https://github.com/blynkkk/blynk-library/blob/master/examples/GettingStarted/BlynkBlink/BlynkBlink.ino#L48)

### LCD
This is a regular 16x2 LCD display made in our secret facility in China.
#### SIMPLE / ADVANCED MODE

#### Commands
You need to use special commands with this widget:

```
lcd.print(x,y, "Your Message");
```
Where x is a symbol position (0-15), y is a line number (0 or 1), 

```
lcd.clear();
```

<img src="images/lcd.png" style="width: 77px;"/>

<img src="images/lcd_edit.png" style="width: 200px;"/>

**Sketch:** [LCD](https://github.com/blynkkk/blynk-library/blob/master/examples/Widgets/LCD/LCD.ino#L22)

### Graph
Easily plot incoming data from your project in various designs.

<img src="images/graph.png" style="width: 77px;"/>

<img src="images/graph_edit.png" style="width: 200px;"/>

**Sketch:** [BlynkBlink](https://github.com/blynkkk/blynk-library/blob/master/examples/GettingStarted/BlynkBlink/BlynkBlink.ino#L48)

### Terminal
Display data from your hardware. Allows also to send any string to your hardware.

You need to use special commands with this widget:

```
terminal.print();
terminal.flush();
```

<img src="images/terminal.png" style="width: 77px;"/>

<img src="images/terminal_edit.png" style="width: 200px;"/>

**Sketch:** [Terminal](https://github.com/blynkkk/blynk-library/blob/master/examples/Widgets/Terminal/Terminal.ino#L23)

##Notifications
###Twitter

Twitter widget connects your Twitter account to Blynk and allows you to send Tweets from your hardware.

<img src="http://static1.squarespace.com/static/54765ba7e4b0d055ee0b47a6/54e92d39e4b0c31341b33a9a/55813d09e4b0ba8aa77ab230/1434533129525/TwitterON.png" style="width: 77px;"/>

<img src="images/twitter_edit.png" style="width: 200px;"/>

Example code:
```cpp
Blynk.tweet("Hey, Blynkers! My Arduino can tweet now!");
```

Limitations :

- you cant' send 2 tweets with same message (it's Twitter policy)
- only 1 tweet per minute is allowed

**Sketch:** [Twitter](https://github.com/blynkkk/blynk-library/blob/master/examples/Widgets/Twitter/Twitter.ino#L26)

###Email

Email widget allows you to send email from your hardware to any address.

<img src="images/mail.png" style="width: 77px;"/>

<img src="images/mail_edit.png" style="width: 200px;"/>

Example code:
```cpp
Blynk.email("my_email@example.com", "Title", "Body");
```

Limitations :

- only 1 email per minute is allowed

**Sketch:** [Email](https://github.com/blynkkk/blynk-library/blob/master/examples/Widgets/Email/Email.ino#L26)

###Push Notifications

Push Notification widget allows you to send push notification from your hardware to your device.

<img src="images/push.png" style="width: 77px;"/>

<img src="images/push_edit.png" style="width: 200px;"/>

Example code:
```cpp
Blynk.notify("Hey, Blynkers! My hardware can push now!");
```

Limitations :

- maximum allowed body length is 255 symbols.
- only 1 notification per minute is allowed

**Sketch:** [PushNotification](https://github.com/blynkkk/blynk-library/blob/master/examples/Widgets/PushNotification/PushNotification.ino#L26)

##Other
###Bridge

Bridge can be used for Device-to-Device communication. You can send digital/analog/virtual write commands from one device to another, knowing it's auth token.

<img src="images/bridge.png" style="width: 77px;"/>

<img src="images/bridge_edit.png" style="width: 200px;"/>

Example code:
```cpp
WidgetBridge bridge1(1); //Bridge widget on virtual pin 1
...
void setup() {
    bridge1.setAuthToken("OtherDeviceAuthToken");
    bridge1.digitalWrite(9, HIGH);
    bridge1.analogWrite(10, 123);
    bridge1.virtualWrite(1, "hello");
}
```

**Sketch:** [Bridge](https://github.com/blynkkk/blynk-library/blob/master/examples/Widgets/Bridge/Bridge.ino#L33)


# Blynk server
Blynk Server is an Open-Source [Netty](https://github.com/netty/netty) based Java server, responsible for forwarding messages between Blynk mobile application and various microcontroller boards (i.e. Arduino, Raspberry Pi. etc).
**Download latest server build [here](https://github.com/blynkkk/blynk-server/releases).**

[ ![Build Status](https://travis-ci.org/blynkkk/blynk-server.svg?branch=master)](https://travis-ci.org/blynkkk/blynk-server)

## Requirements
Java 8 required. (OpenJDK, Oracle). Installation instructions [here](https://github.com/blynkkk/blynk-server#install-java-for-ubuntu).

## Getting Started
By default, mobile application uses 8443 port and is based on SSL/TLS sockets. Default hardware port is 8442 and is based on plain TCP/IP sockets.

### Quick local server setup

1. Make sure you are using Java 8

        java -version
        Output: java version "1.8.0_40"

2. Run the server on default 'hardware port 8442' and default 'application port 8443' (SSL port)

        java -jar server-0.8.2.jar -dataFolder /path
        
	That's it! You won't see any output because all the logging is done within same folder in ```./logs/blynk.log file```.

### Quick local server setup on Raspberry PI

1. Login to Raspberry Pi via ssh;
2. Install java 8 : 
        
        sudo apt-get install oracle-java8-jdk
        
3. Make sure you are using Java 8

        java -version
        Output: java version "1.8.0_40"
        
4. Download Blynk server jar file (or manually copy it to raspberry via ssh and scp command) : 
   
        wget "https://github.com/blynkkk/blynk-server/releases/download/v0.8.2/server-0.8.2.jar"

5. Run the server on default 'hardware port 8442' and default 'application port 8443' (SSL port)

        java -jar server-0.8.2.jar -dataFolder /home/pi/Blynk        
        
You won't see any output because all logging is done within same folder in: ```./logs/blynk.log file```.
        
To enable server auto restart find /etc/init.d/rc.local file and add:

```
java -jar /home/pi/server-0.8.2.jar -dataFolder /home/pi/Blynk &
```
                
### App settings and sketch changes

1. Specify custom server path in Blynk app when logging in.

<img src="images/login.png" style="width: 200px;"/>  <img src="images/custom.png" style="width: 200px;"/>

2. Change your Ethernet sketch from

```
Blynk.begin(auth);
```

to

```
Blynk.begin(auth, "your_host");
```
or ```Blynk.begin(auth, IPAddress(xxx,xxx,xxx,xxx));```    

Change your WIFI sketch from:

```        
Blynk.begin(auth, SSID, pass));
```

to

```
Blynk.begin(auth, SSID, pass, "your_host");
```
or to

```Blynk.begin(auth, SSID, pass, IPAddress(XXX,XXX,XXX,XXX));```

If you are connected via USB, when running ```blynk-ser.sh``` provide ```'-s'``` option with address of your local server: 

```bash
./blynk-ser.sh -s you_host_or_IP
```        

## Advanced local server setup
If you need more flexibility, you can extend server with more options by creating server.properties file in same folder as server.jar. Example could be found [here](https://github.com/blynkkk/blynk-server/blob/master/server/tcp-server/src/main/resources/server.properties).
server.properties options:

+ Application port

        app.ssl.port=8443
        
+ For simplicity, Blynk provides server jar with already built-in SSL certificates, so you have working server out-of-the box via SSL/TLS sockets. But since certificate and it's private keys are in public, it makes it completely unsecure. 

	In order to fix that you need to provide your own certificates. And change properties below with a path to your certificates, private key and it's password. 
	See how to generate self-signed certificates [here](https://github.com/blynkkk/blynk-server#generate-ssl-certificates)

        #points to cert and key that placed in same folder as running jar.
        
        server.ssl.cert=./server_embedded.crt
        server.ssl.key=./server_embedded.pem
        server.ssl.key.pass=pupkin123

+ Hardware port

        hardware.default.port=8442

+ User profiles folder. Folder in which all users profiles will be stored. By default System.getProperty("java.io.tmpdir")/blynk used. Will be created if not exists

        data.folder=/tmp/blynk

+ Folder for all application logs. Will be created if it doesn't exist

        logs.folder=./logs

+ Log debug level. Possible values: trace|debug|info|error. Defines how precise logging will be. From left to right -> maximum logging to minimum

        log.level=trace

+ Maximum allowed number of user dashboards.

        user.dashboard.max.limit=10

+ 100 Req/sec rate limit per user.

        user.message.quota.limit=100

+ In case user exceeds quota limit - response error returned only once in specified period (in Millis).

        user.message.quota.limit.exceeded.warning.period=60000

+ Maximum allowed user profile size. In Kb's.

        user.profile.max.size=128

+ Maximum allowed number of notification queue. Queue responsible for processing email, pushes, twits sending. Because of performance issue - those queue is processed in separate thread, this is required due to blocking nature of all above operations. Usually limit shouldn't be reached
        
        notifications.queue.limit=10000

+ Period for flushing all user DB to disk. In millis

        profile.save.worker.period=60000

+ Specifies maximum period of time when application socket could be idle. After which socket will be closed due to non activity. In seconds. Leave it empty for infinity timeout

        app.socket.idle.timeout=600

+ Specifies maximum period of time when hardware socket could be idle. After which socket will be closed due to non activity. In seconds. Leave it empty for infinity timeout

        hard.socket.idle.timeout=15
        
+ Mostly required for local servers setup in case user want to log raw data in CSV format. See [raw data] (https://github.com/blynkkk/blynk-server#raw-data-storage) section for more info.
        
        enable.raw.data.store=true
        
+ Comma separated list of users allowed to create accounts. Leave it empty if no restriction required.
        
        allowed.users.list=allowed1@gmail.com,allowed2@gmail.com
        
### Enabling e-mail on Local server
In order to enable mail notifications on Local server you need to provide own mail credentials. To do that you need to create file "mail.properties" within same folder where server.jar is.
Mail properties :

	mail.smtp.auth=true
	mail.smtp.starttls.enable=true
	mail.smtp.host=smtp.gmail.com
	mail.smtp.port=587
	mail.smtp.username=YOUR_EMAIL_HERE
	mail.smtp.password=YOUR_EMAIL_PASS_HERE
        
See example [here](https://github.com/blynkkk/blynk-server/blob/master/server/notifications/mail-notifications/src/main/resources/mail.properties).

NOTE : you'll need to setup Gmail to allow less secured applications. Go [here](https://www.google.com/settings/security/lesssecureapps) and then click "Allow less secure apps".


## Raw data storage
By default raw data storage is enabled. So any write (Blynk.virtualWrite) command will stored on disk. 
The default path is "data" folder within [data.folder] (https://github.com/blynkkk/blynk-server#advanced-local-server-setup) property of server properties.

File name format is 
        
	dashBoardId_pin.csv

For instance
 
	data/1_v5.csv
        
Which means in 1_v5.csv file stored raw data for virtual pin 5 of dashboard with id 1.

Data format is

	value,timestamp
        
For instance

	10,1438022081332
        
Where 10 - value of pin, and 1438022081332 - the difference, measured in milliseconds, between the current time and midnight, January 1, 1970 UTC.

Raw data files are rotated every day and gzipped.

WARNING : this will changed in near future. 

## Generate SSL certificates

1. Create key

		openssl genrsa -out server.key 2048
        
2. Create new cert request
        
		openssl req -new -out server.csr -key server.key

3. Generate self-signed request

		openssl x509 -req -days 1825 -in server.csr -signkey server.key -out server.crt
        
4. Convert server.key to PKCS#8 private key file in PEM format

		openssl pkcs8 -topk8 -inform PEM -outform PEM -in server.key -out server.pem
        
WARNING : in case you connect hardware via [USB script](https://github.com/blynkkk/blynk-library/tree/master/scripts) you have to provide an option '-s' pointing to "common name" (hostname) you did specified during certificate generation.
        
As output you'll retrieve server.crt and server.pem files that you need to provide for server.ssl properties.

### Install java for Ubuntu

    sudo apt-add-repository ppa:webupd8team/java
    sudo apt-get update
    sudo apt-get install oracle-java8-installer

## Behind wifi router
If you want to run Blynk server behind WiFi-router and want it to be accessible from the Internet, you have to add port-forwarding rule on your router. This is required in order to forward all of the requests that come to the router within the local network to Blynk server.

## Performance
Currently server handles 20k req/sec with SSL and 40k req/sec without SSL hardware messages on VM with 2-cores of Intel(R) Xeon(R) CPU E5-2660 @ 2.20GHz. With high load - memory consumption could be up to 1 GB of RAM.

## App Client (emulates Smartphone App)

1. Start simulator of Smartphone App client:

        java -jar client-${PUT_LATEST_VERSION_HERE}.jar -mode app -host localhost -port 8443


2. When client started, register new user and/or login using this credentials:

        register username@example.com UserPassword
        login username@example.com UserPassword


3. Save profile with simple dashboard

        saveProfile {"dashBoards":[{"id":1, "name":"My Dashboard", "boardType":"UNO"}]}


4. Get the Auth Token for hardware (e.g Arduino):

        getToken 1

5. Activate dashboard (equals to PLAY button in the app)

        activate 1

You will get server response similar to this:

	00:05:18.100 TRACE  - Incomming : GetTokenMessage{id=30825, command=GET_TOKEN, length=32, body='33bcbe756b994a6768494d55d1543c74'}

Where `33bcbe756b994a6768494d55d1543c74` is your Auth Token.

## Hardware Client (emulates Hardware)

Start new client and use Auth Token from previous step to login:

	java -jar client-${PUT_LATEST_VERSION_HERE}.jar -mode hardware -host localhost -port 8442
    	login 33bcbe756b994a6768494d55d1543c74
   

You can run as many clients as you want.

Clients with the same credentials and Auth Token are grouped into one Session and can send messages to each other.
All client’s commands are human-friendly, so you don't have to remember the codes.

## Hardware Commands

Before sending any read/write commands to hardware, application must first send “init” command.
"Init" command is a 'hardware' command which sets all the Pin Modes(pm). Here is an example of "init" command:

    hardware pm 1 in 13 out 9 out 8 in

// TODO: take description about pin modes from Blynk Arduino library readme
// TODO Describe separation with Zeroes in pinmode command

In this example you set pin 1 and pin 8 to 'input’ PIN_MODE. This means this pins will read values from hardware (graph, display, etc).
Pins 13 and 9 have 'output’ PIN_MODE. This means that these pins will we writable (button, slider).

List of hardware commands:

+ Digital write:

		hardware dw 9 1
    	hardware dw 9 0


+ Digital read:

    	hardware dr 9
    	You should receive response: dw 9 <val>


+ Analog write:

    	hardware aw 14 123


+ Analog read:

    	hardware ar 14
        You should receive response: aw 14 <val>


+ Virtual write:

    	hardware vw 9 1234
        hardware vw 9 string
        hardware vw 9 item1 item2 item3
        hardware vw 9 key1 val1 key2 val2

 
+ Virtual read:

    	hardware vr 9
    	You should receive response: vw 9 <values>

#Security

Blynk server has 3 ports open for different security levels.

* **8441** - SSL/TLS connection for hardware
* **8442** - plain TCP connection for hardware (no security)
* **8443** - mutual authentication (mutual SSL) connection for Mobile Apps

Hardware may select to connect to 8441 or 8442, depending on it's capabilities.

## SSL gateway

Most platforms are not capable to handle SSL, so they connect to 8442.
However, our [gateway script](https://github.com/blynkkk/blynk-library/blob/master/scripts/blynk-ser.sh) can be used to add SSL security layer to communication.

```bash
./blynk-ser.sh -f SSL
```
This will forward all hardware connections from 8441 port to the server via SSL gateway.
You can run this script on your Raspberry Pi, desktop computer, or even directly on your router!

**Note:** when using your own server, you should overwrite the bundled server.crt certificate, or specify it to the script using ```--cert``` switch:

```bash
./blynk-ser.sh -f SSL -s <server ip> -p 8441 --cert=<certificate>.crt
```

Flag ```-f SSL``` is enabled by default for USB communication so you don't have to explicit declare it.

**Note:** SSL is supported by the gateway only on Linux/OSX for now
 
If you want to skip SSL, and connect to TCP, you can also do that:

```bash
./blynk-ser.sh -t TCP
```

### Local Blynk Server

In order to gain maximum security you could [install Blynk server locally](https://github.com/blynkkk/blynk-server#blynk-server) and restrict access to your network, so nobody except you could access it.


# Troubleshooting

## Connection

If you experience connection problems, follow these steps:

1. Check your wiring using the examples (TCP/HTTP Client or similar) **provided with selected shield and hardware**.     Once you have some understanding how to configure connection, it's much easier to use Blynk.
2. Try running Blynk default examples for your platform **without modifications** to see if it is working.
   * Read carefully the example comments and explanations
   * Check that your token is valid (copied from the App and **doesn't contain spaces, etc.**)
   * If it doesn't work, try looking into [serial debug prints](./Troubleshooting.md#enable-debug).
3. Done! Add your modifications and functionality. Enjoy Blynk!

## Delay

Your application might be calling a delay() function or sleeps/cycles for a long time inside of the loop(), like this:

```cpp
void loop()
{
  ...
  delay(1000);
  other_long_operation();
  ...
  Blynk.run();
}
```
    
You should be aware that this can degrade performance of Blynk, or cause connection drops.

**Note:** This also applies to the BLYNK_READ & BLYNK_WRITE handlers!

If you need periodic actions, consider using some timer library, like shown [in this example](https://github.com/blynkkk/blynk-library/blob/master/examples/GettingStarted/PushData/PushData.ino).

## Flood Error

Your application may cause an enormous load on our server, please try avoiding sending data too fast.

For example, in this situation Blynk.run() will quickly finish processing incoming messages, and then new value is sent to the server immediately, causing high traffic:

```cpp
void loop()
{
  Blynk.virtualWrite(1, value);
  Blynk.run();
}
```

You might be thinking about adding a delay(), but this creates [another trouble](./Troubleshooting.md#delay).

If you need periodic actions, consider using some timer library, like shown [in this example](https://github.com/blynkkk/blynk-library/blob/master/examples/GettingStarted/PushData/PushData.ino).

### Enable debug

To enable debug prints on the default Serial, add on the top of your sketch **(should be the first line
)**:

```cpp
#define BLYNK_DEBUG // Optional, this enables lots of prints
#define BLYNK_PRINT Serial
```
And enable serial in setup():

```cpp
Serial.begin(9600);
```

You can also use spare Hardware serial ports or SoftwareSerial for debug output (you will need an adapter to connect to it with your PC).

**Note:** enabling debug mode will slowdown your hardware processing speed up to 10 times.

# Implementing a Blynk HW client (library)
Here is an information on how to write a custom library.

Currently we provide Arduino/C++ implementation of the library.
It is very extensible and modular, look at [the list of supported hardware](http://blynkkk.github.io/#list-of-supported-hardware).
Adding new connection types and Arduino-compatible boards is easy.

TODO: Porting guide.

But some devices are programmed in other languages, like:

* Espruino, JavaScript, Node.JS
* MicroPython, Python
* NodeMCU, eLua

## Blynk library main functions

- Provide easy-to use API
 * Virtual pin handlers registration
 * Provide comfortable wrappers for some widgets
* Manage connection
 * Should support different connection type/hardware, if applicable
* Serialize/deserialize Blynk protocol
* Handle direct pin operations
* Should be portable across similar devices (or same technology/programming language), if possible
* Should detect and notify the user about [troubles](http://blynkkk.github.io/#troubleshooting) where possible (especially Flood)

### Hardware Description file
Blynk Apps use this JSON file to correctly work with all the variety of hardware. It's like a pinout diagram with some additonal information. 


```json
{
    "name": "Arduino UNO",
    "map": {
        "digital": {
            "pins": {
                "D0":  0,  "D1":  1,  "D2":  2,  "D3":  3, "D4": 4,
                "D5":  5,  "D6":  6,  "D7":  7,  "D8":  8, "D9": 9,
                "D10": 10, "D11": 11, "D12": 12, "D13": 13
            },
            "ops": [ "dr", "dw" ]
        },
        "analog": {
            "pins": {
                "A0": 14, "A1": 15, "A2": 16, "A3": 17, "A4": 18, "A5": 19
            },
            "ops": [ "dr", "dw", "ar" ],
            "arRange":[0, 1023]
        },
        "pwm": {
            "pins": [
                "D3", "D5", "D6", "D9", "D10", "D11"
            ],
            "ops": [ "aw" ],
            "awRange":[0, 255]
        },
        "virtual":  {
            "pinsRange": [ 0, 31 ],
            "ops": [ "vr", "vw" ]
        }
    }
}
```

Look at the [full boards list](https://github.com/blynkkk/blynk-library/tree/master/boards_json).
You can send us your own board description file for review and App integration.

There may be a problem that you want to start testing your implementation, but your board is not listed int the Blynk App.
On Android, we now have a "Generic Board" specially for such purposes.
Unfortunately iOS does not have it yet.

Basically you can select UNO board and check how it works using just virtual pins.
Most digital pins will also work.
Analog IO/PWM will not work in general, until we add your board to the App.

# Blynk protocol

Blynk transfers binary messages with the following structure:

| Command       | Message Id    | Length/Status   | Body     |
|:-------------:|:-------------:|:---------------:|:--------:|
| 1 byte        | 2 bytes       | 2 bytes         | Variable |

Message Id and Length are [big endian](http://en.wikipedia.org/wiki/Endianness#Big-endian).
Body has a command-specific format.

Command and Status definitions: [BlynkProtocolDefs.h](https://github.com/blynkkk/blynk-library/blob/master/Blynk/BlynkProtocolDefs.h)

Another protocol description can be found [here](https://github.com/blynkkk/blynk-server/blob/master/README_FOR_APP_DEVS.md#protocol-messages).

Typical Blynk library knows how to send(S)/process(P):

    S   BLYNK_CMD_LOGIN + auth token
    SP  BLYNK_CMD_PING
    SP  BLYNK_CMD_RESPONSE
    SP  BLYNK_CMD_BRIDGE
    SP  BLYNK_CMD_HARDWARE
    S   BLYNK_CMD_TWEET
    S   BLYNK_CMD_EMAIL
    S   BLYNK_CMD_PUSH_NOTIFICATION

## HARDWARE/BRIDGE command body

The body of these commands are encoded as a sequence of strings, separated by ```'\0'``` ([Null character](http://en.wikipedia.org/wiki/Null_character)).
Please note that the last value may be not Null-terminated.
In the following command examples ```\0``` chars are replaced with spaces.

### Pin mode

PinMode command is received by library after connection, or when a mobile application starts.

    pm <pin> <mode>
    pm <pin> <mode> <pin> <mode> <pin> <mode> ...

Mode:

* in - INPUT
* out - OUTPUT
* pu - INPUT_PULLUP
* pd - INPUT_PULLDOWN

### Digital pin operations

Digital write:

    dw <pin> <val>

Digital read:

    dr <pin>

### Analog pin operations

    aw <pin> <val>

    ar <pin>

### Virtual pin operations

    vw <pin> <param0> <param1> <param2> <param3> ...

    vr <pin>

### Other operations

    info

TODO

## Developer notes

* Values in HW commands are plain text.
* In response to ```dr/ar``` command, library should send ```dw/aw``` command on the same pin and with the same message id.
* These situations should cause a connection drop, or reconnection attempt:
 * Message with ```ID=0``` is received
 * Message with unknown type is received
 
## Adding network interface 
4 entities should be created to add a new network interface to Blynk:
 
1. Select connection interface that will be used for Blynk operation.  
   This should be something like http://www.arduino.cc/en/Tutorial/WebClient  
   Based on the API of the connection, create the **Transport**.  
   Some examples may be found in the Adapters folder:
   * BlynkTransportSerial
   * BlynkTransportCC3000
   * BlynkArduinoClient - *can be reused, if possible*
   
2. Create **Blynk representative class**, which contains connection-specific helper functions (like begin).
   Examples:
   * BlynkEthernet
   * BlynkSerial
   * BlynkCC3000
   * BlynkWildFire
   * BlynkYun
   
3. Create **BlynkSimple*** header for your connection.  
   This constructs main **Blynk instance**, so the user (mostly) doesn't need to get into such details.  
   Examples:
   * BlynkSimpleEthernet.h
   * BlynkSimpleCC3000.h
   * BlynkSimpleWifi.h
   * BlynkSimpleUIPEthernet.h
   
4. Create a **simple example** for your platform ;)

### Example implementations
Use these to play with the protocol and understand the basics:

* [Pseudo-library in Python](https://github.com/blynkkk/blynk-library/blob/master/tests/pseudo-library.py)
* [Node.js + Espruino](https://github.com/vshymanskyy/blynk-library-js)
* [Arduino](https://github.com/blynkkk/blynk-library)
* [Particle Core](https://github.com/vshymanskyy/blynk-library-spark)


#Blynk Amendments
###Tell every maker about Blynk
No pressure. Just do it. Now.
###Make your idea work without Blynk
Blynk can be easily integrated in almost any project. But before that - make it work **without** it. After you are sure that you can get all the sensor data or can control things from the code – integrate Blynk and make it even more awesome.
###Use search
We are always happy to chat and help, but remember - every time you ask the question that was answered many many times before that, Blynk Team is not building a new widget or new cool feature. So:
- google before asking
- use search on our forum, it works really well
- check Instructables
###Always wrap your code
Though shalt not post code without ```wrapping it``` 