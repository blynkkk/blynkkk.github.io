#Intro
A few words about Blynk. Contents?

<img src="https://github.com/blynkkk/blynkkk.github.io/blob/master/images/blynk_architecture.png" style="width: 450px;"/>



#Getting Started
###Download all the ingridients:
**Blynk App for iOS or Android:** <br> <br> 
[<img src="http://static1.squarespace.com/static/54765ba7e4b0d055ee0b47a6/t/55515fd0e4b08237a78598e2/1431396305454/?format=500w" alt="Drawing" style=" width: 150px;"/>](https://itunes.apple.com/us/app/blynk-control-arduino-raspberry/id808760481?ls=1&mt=8)  &nbsp; &nbsp; &nbsp; &nbsp;[<img src="http://static1.squarespace.com/static/54765ba7e4b0d055ee0b47a6/t/55515fe8e4b08237a785995e/1431396357648/?format=750w" alt="Drawing" style=" width: 200px;"/>](https://play.google.com/store/apps/details?id=cc.blynk)

**Install Blynk Library:** <br><br>
[Download Blynk Library >](https://github.com/blynkkk/blynk-library/archive/v0.2.4.zip)

In case you forgot how to install Arduino libraries: check [here](http://www.arduino.cc/en/guide/libraries).  We are also good friends of **[codebender](https://codebender.cc/example/BlynkSimpleEthernet/GettingStarted:BlynkBlink)** - you can code and upload Blynk sketches to your hardware directly from your browser.

###Blink With Blynk 

Let's turn LED connected to your hardware ON and OFF with the Blynk App

>result animated gif/instagram

Use this wiring scheme to connect LED to your board:

<img src="http://faberfun.com/wp-content/uploads/2013/08/Blink-LED-using-Arduino-uno.jpg" alt="Drawing" style="width: 250px;"/>

### Create Blynk Account In The App
<img src="https://github.com/blynkkk/blynkkk.github.io/blob/master/images/sign_up.png"/>


### IAuth Token
**Auth Token** is used to connect your Arduino or other board to your smartphone. Every new project you create will have an Auth Token. 

>Screenshot / animation

It's very convenient to send it over E-mail. If you press E-mail button – token will be sent to the e-mail address you used for registration. If you have a good memory - you can memorize it ;) or tap the number and it will be copied to the clipboard.


### Choose your hardware
Select the hardware you are building project on.

# Let's Get Online
You know that **Blynk works over the Internet**, right? (Bluetooth LE is on the way) 

Blynk works with almost anything, check the [full list of supported hardware]()


Before you start Blynking, you need to understand how you will connect to the Internet. It can be an Ethernet Shield for Arduino, or may be your hardware is already internet-enabled (e.g. Spark Core). 


### How To Use Example Sketches
> Illustration 
> Building Blocks:
> 
> * Connection Layer
> * Auth Token
> * Processing Layer

### Choosing Your Connection Type 
We've prepared example sketches which will get your microcomputer online. Open the example sketch according to your device or shield. If you are using **codebender** - find the example you need in the [list]()


<img src="http://static1.squarespace.com/static/54765ba7e4b0d055ee0b47a6/54e92d39e4b0c31341b33a9a/557c3b82e4b0ff7f4a641ca4/1434205059233/Screen+Shot+2015-06-13+at+4.11.33+PM.png?format=500w" style="width: 500px;"/>

###Insert Auth Token

As it was said prevously, Auth Token is used to identify your hardware and connect it with the smartphone. 

In the example sketch find this line in code:


```
char auth[] = "Your AuthToken";

```

Change it by putting your Auth Token inside curly brackets. 

``` 
char auth[] = "123456789abcdefghijk0987654321";

```
If you don't know what is your [Auth Token](https://github.com/blynkkk/blynkkk.github.io#auth-token) for the project - check the Project Settings in the app. You can send it over the E-mail. 

>Screenshot from the app


Never post your Auth Token publically, unless you want other people to be able to connect to your project. 

Upload sketch to the board and open Serial Terminal. Wait until you see something like this: 

``` 
Your IP is 192.168.0.11
Connecting...
Blynk connected!

```

### <span style="color:#24C48C" >**Congratulations! It was the hardest part and it's over!**</span>



### Connect over USB,  and others

If you don't have any shield and your hardware doen's have any connectivity, you can still use Blynk – directly over USB. It's a bit tricky for newbies, but if you follow these [USB instructions](link) you'll succeed for sure. We also work on enhancing this process.

###Raspberry Pi, Spark Core
* **Spark Core** owners: check [here]()
* **Raspberry Pi** eaters: [here]() 


# Set Up Your Project

Open your project in the app. It's empty now, so let's add a Button. Just tap anywhere on empty space - Widget Box will open. Choose the Button Widget.

> Screenshot

Hold and drag it to reposition

> Screenshot

Tap on the widget to get to it's settings  

> Screenshot

The most important parameter to set is **PIN** . List of pins reflects physical pins defined by your hardware. If your LED is connected to Digital Pin 10 - then select **D10** (**D** - stands for **D**igital). Virtual pins are described [here]().    

> Illustration showing how Physical PIN is connected to Pin in the APP.

When you are done with the Settings - press **PLAY** button. This will switch you from EDIT mode to PLAY mode where you can interact with widgets. You can always get back to EDIT mode by pressing STOP

> Screenshot

Press Button to turn the LED On and Off

> Screenshot

Always feel free to experiment! For example, attach an LED to [PWM](http://www.arduino.cc/en/Tutorial/Fading)-enabled Pin on your Arduino. Set the Slider Widget to control brightness of an LED. Just use the same steps described above.

**Happy Blynking!**

# Blynk Basics

You can find example sketches covering basic Blynk Features. They are included in the libary. All the sketches are designed to be easily combined with each other. 


### Virtual Pins
Virtual Pins are designed to send **any data** from your microcontroller to the Blynk App and vice versa. 
Think about Virtual Pins as channels for any variables. Don't 

Make sure you differentiate Virtual Pins from physical pins on your Arduino. Virtual Pins have no physical representation, they exist only in code. 

Virtual Pin 5 in the App will write to Virtual Pin 5 on the hardware

>Illustration showing Virtual Pin

There are 32 Virtual pins at your disposal (V0 - V31)
> screenshot of pin picker 

Virtual Pins is a powerful feature. Learn what you can do with them:

### Reading Blynk App Data
All Output Widgets can write data to Virtual Pins. Just tell Arduino which pin to READ, using this code: 

<span style="color:#D3435C;"> ---------CHANGE CHANGE CHANGE: 
WRITE CHANGED to READ because it's way easier to explain ------------</span> 

```
BLYNK_READ(pinNumber)
{
  pinData = param.asInt()); 
}
```

<span style="color:#D3435C;">**NOTE:** This construction should be always placed **outside** of any loop</span> 

You can interpret incoming data as INTs, Floats, Doubles and Strings:

```
  param.asInt());
  param.asFloat());
  param.asDouble());
  param.asStr());
```
 
Some Widgets (e.g Joystick, zeRGBa) have more than one output. This output is an array of values. You can get any parameter of the array [0,1,2...] by using: 

```
BLYNK_READ(pinNumber)
{   
  pinData = param(1).asInt());
}
```
Using Virtual Pins for Widgets with multiple outputs will improve performance.

### Pushing Data to the Blynk App

There are two ways of pushing data from your hardware to the Widgets in the app over Virtual Pins. 

1. **Using Blynk built-in reading frequency**
2. **Writing your own logic of pushing data**



Most flexible way to push data to the app is using:

Optinally: *If you need to push processed data from your hardware to the Blynk App, use Virtual Pins to do it.*

```
Blynk.virtualWrite(pinNumber, value);
```
In the Widget, choose the **same** Virtual Pin and set Reading Frequency parameter to PUSH

>Screenshot of the Frequency

There are some requirements when using this command. Please read carefully through them:

We suggest you to use **[SimpleTimer]()** library for events that are executed in intervals. Read instructions inside this [example sketch]() for more details.

1. Don't put ```Blynk.virtualWrite``` inside ```void loop()```. This will cause lot's of outgoing messages to our server and your connection will be terminated.
2. Avoid using long delays with ```delay()``` – it may cause connection breaks
3. <span style="color:#000000;">Don't send more that 10 values per second** - otherwise you'll get **FLOOD** error and your connection will be terminated.</span>


# Raspberry Pi
Specific steps for Raspberry Pi

# Spark Core
Specific steps for Spark Core


#List Of Supported Hardware
List of devices goes here


#Widgets
### Common Widget Settings
Most of the settings are self-explanatory, but there are some hidden features that you can use.

### Pin Selection
This is one of the main parameters you need to set
>Screenshot

Read more about Virtual Pins Here

### Data Mapping
>Screenshot

### Splitting/Merging Outputs
>Screenshot


Controls:
### Button
>Image

### Slider
>Image

### Timer
>Image

### Joystick
>Image

Displays:
### Value Display
>Image

### Graph
>Image

### LCD Display
>Image

Notifications:
### Twitter

Twitter Widget connects your Twitter account to Blynk and allows you to send Tweets from your hardware. 

<img src="http://static1.squarespace.com/static/54765ba7e4b0d055ee0b47a6/54e92d39e4b0c31341b33a9a/55813d09e4b0ba8aa77ab230/1434533129525/TwitterON.png" style="width: 77px;"/>


Example code:

```
if (something) 
{
   Blynk.tweet("Hey, Blynkers! My Arduino can tweet now!");
}

```

### Email
>Image

### Push Notifications
>Image


#Blynk Commands
The library can perform basic pin IO (input-output) operations out-of-the-box:

```
digitalRead
digitalWrite
analogRead
analogWrite //PWM or Analog signal depending on the platform
```

### BLYNK_WRITE(vPIN)
### BLYNK_READ(vPIN)
### Blynk.virtualWrite();

You can send all the formats of data to Virtual Pins

```
Blynk.virtualWrite(pin, "abc");
Blynk.virtualWrite(pin, 123);
Blynk.virtualWrite(pin, 12.34);
```

### BLYNK_PRINT
### BLYNK_LOG
### BLYNK_CONNECT();
### BLYNK_DEBUG
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

### Blynk.notification("message");
### Blynk.email();
In order to use this command, you need to add Email Widget in the App

Send a pre-defined email message

```Blynk.email();```

Send an email message with custom body:

```Blynk.email("Message");```

Send an email message with custom body, subject and recipient:

```Blynk.email("email@example.com", "Subject", "Message");```





#Blynk API. Writing your own library
Instructions on how to add support for new hardware 


#Security

Blynk server has 3 ports open for different security levels.
* 8441 - SSL/TLS connection for hardware
* 8442 - plain TCP connection for hardware (no security)
* 8443 - mutual authentication (mutual SSL) connection for Mobile Apps

Hardware may select to connect to 8441 or 8442, depending on it's capabilities.

### SSL gateway

Most platforms are not capable to handle SSL, so they connect to 8442.
However, our [gateway script](https://github.com/blynkkk/blynk-library/blob/master/scripts/blynk-ser.sh) can be used to add SSL security layer to communication.

```bash
./blynk-ser.sh -f SSL
```
This will forward all hardware connections from 8441 port to the server via SSL gateway.
You can run this script on your Raspberry Pi, desktop computer, or even directly on your router!

**Note:** when using your own server, you should overwrite the bundled server.crt certificate, or specify it to the script using --cert switch:

```bash
./blynk-ser.sh -f SSL -s <server ip> -p 8441 --cert=<certificate>.crt
```

Flag "-f SSL" is enabled by default for USB communication so you don't have to explicit declare it.
**Note:** SSL is supported by the gateway only on Linux/OSX for now
 
If you want to skip SSL, and connect to TCP, you can also do that:

```bash
./blynk-ser.sh -t TCP
```

### Local Blynk Server

In order to gain maximum security you could install Blynk server locally and restrict access to your network, so nobody except you could access it.
See how to install Blynk server locally [here](https://github.com/blynkkk/blynk-server#blynk-server).


# Troubleshooting

### Connection

If you experience connection problems, follow these steps:

1. Check your wiring using the examples (TCP/HTTP Client or similar) **provided with selected shield and hardware**.     Once you have some understanding how to configure connection, it's much easier to use Blynk.
2. Try running Blynk default examples for your platform **without modifications** to see if it is working.
   * Read carefully the example comments and explanations
   * Check that your token is valid (copied from the App and **doesn't contain spaces, etc.**)
   * If it doesn't work, try looking into [serial debug prints](./Troubleshooting.md#enable-debug).
3. Done! Add your modifications and functionality. Enjoy Blynk!

### Delay

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

### Flood

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




#Links

* [Kickstarter campaign](https://www.kickstarter.com/projects/167134865/blynk-build-an-app-for-your-arduino-project-in-5-m/description)
* [Blynk downloads, docs, tutorials](http://www.blynk.cc)
* [Blynk community](http://community.blynk.cc)
* [Facebook](http://www.fb.com/blynkapp)
* [Twitter](http://twitter.com/blynk_app)

# License

This project is released under The MIT License (MIT)


# Other Docs

* [Basics](./docs/Basics.md)
* [Widgets](./docs/Widgets.md)
* [Security](./docs/Security.md)
* [Platforms/Connection types](./docs/Platforms.md)
* [Troubleshooting](./docs/Troubleshooting.md)
* [Implementing your own library](./docs/Implementing.md)
