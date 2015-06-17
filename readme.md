#Intro
A few words about Blynk. Contents?

<img src="https://ksr-ugc.imgix.net/assets/003/046/877/1c622f9beb988b1619213b345e5b8639_original.png?v=1418594107&w=680&h=&fit=max&auto=format&lossless=true&s=a7e09be913cdc24a7e7e62939c988c90" style="width: 500px;"/>



#Getting Started
###Download all the ingridients:
**Blynk App for iOS or Android:** <br> <br> 
[<img src="http://static1.squarespace.com/static/54765ba7e4b0d055ee0b47a6/t/55515fd0e4b08237a78598e2/1431396305454/?format=500w" alt="Drawing" style=" width: 150px;"/>](https://itunes.apple.com/us/app/blynk-control-arduino-raspberry/id808760481?ls=1&mt=8)  &nbsp; &nbsp; &nbsp; &nbsp;     [<img src="http://static1.squarespace.com/static/54765ba7e4b0d055ee0b47a6/t/55515fe8e4b08237a785995e/1431396357648/?format=750w" alt="Drawing" style=" width: 200px;"/>](https://play.google.com/store/apps/details?id=cc.blynk)

**Install Blynk Library:** <br><br>
[Download Blynk Library >](https://github.com/blynkkk/blynk-library/archive/v0.2.1.zip)

In case you forgot how to install Arduino libraries: check [here](http://www.arduino.cc/en/guide/libraries).  We are also good friends of **[codebender](https://codebender.cc/example/BlynkSimpleEthernet/GettingStarted:BlynkBlink)** - you can code and upload Blynk sketches to your gardware directly from your browser.

###Blink With Blynk 

Let's start with something easy: turn LED connected to your hardware ON and OFF with the Blynk App

>animated gif

Use this wiring scheme to connect LED to your Hardware:

<img src="http://faberfun.com/wp-content/uploads/2013/08/Blink-LED-using-Arduino-uno.jpg" alt="Drawing" style="width: 250px;"/>

### Create Blynk Account In The App
>Screenshot / Animation


###Auth Token
**Auth Token** is used to connect your Arduino or other board to your smartphone. Every new project you create will have an Auth Token. 

>Screenshot / animation

It's very convenient to send it over E-mail. If you press E-mail button – token will be sent to the e-mail address you used for registration. If you have a good memory - you can memorize it ;) or tap the number and it will be copied to the clipboard.


### Choose your hardware
Select the hardware you are building project on.

#Let's Get Online
You know that **Blynk works over the Internet**, right? (Bluetooth LE is on the way) 

Blynk works with almost anything, check the [full list of supported hardware]()


Before you start Blynking, you need to understand how you will connect to the Internet. It can be an Ethernet Shield for Arduino, or may be your hardware is already internet-enabled (e.g. Spark Core). 


###How To Use Example Sketches
> Illustration 
> Building Blocks:
> 
> * Connection Layer
> * Auth Token
> * Processing Layer

###Choosing Your Connection Type 
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



###Connect over USB,  and others

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

#Blynk Basics

We prepared example sketches to show main Blynk Features. All the sketches are designed so that it's easy to combine one example with another. 


###Virtual Pins
Virtual Pins are designed to send **any data** from microcontroller to the Blynk app and back. 
Think about Virtual Pins as channels for any variables. They are different to physical pins on your Arduino. 
>Illustration showing Virtual Pin

There are 32 Virtual pins at your disposal (V0 - V31)
> screenshot of pin picker 



``` 
Blynk.virtualWrite(PIN, VALUE)

```


###Send data from Arduino to Smartphone with Virtual Pin

>Let's say you want to send convert data from temperature sensor from ºC to ºF and send it to Blynk every 1 second.

Open the sketch accordingly to your hardware. This example is for [Ethernet Shield]()

To avoid using ```delay();``` function, which may cause connection interruptions, we recommend using **[SimpleTimer]()** library for events that need intervals. Check this [example sketch]() for more details.


<span style="color:red;">**Don't send more that 10 values per second** - otherwise you'll get **FLOOD** warning and your messages will be banned</span>



```
void yourTimedEvent()
{
  Blynk.virtualWrite(5, something;)
}

void loop()
{
  Blynk.run(); 
  timer.run(); 
}
```

#### How to process data from Blynk App on Arduino
You can use any data from Blynk in your project by using Virtual Pins


```
BLYNK_WRITE(1)
{
  BLYNK_LOG("Got a value: %s", param.asStr());
}
```

This command means that hardware is listening to the Widget, that WRITEs data to Virtual Pin 1 in the app.

You can get data as INTs, Floats, Doubles and Strings 

```
  param.asInt());
  param.asFloat());
  param.asDouble());
  param.asStr());
```
 
Some Widgets may send an array of values (e.g Joystick, zeRGBa). You can get any parameter of the array by using: 

```
BLYNK_WRITE(1)
{   
  BLYNK_LOG("Got a value: %s", param(2).asInt());
}
```


# Running Blynk on Raspberry Pi and Spark Core
Specific steps for Raspberry Pi

Specific steps for Spark Core 

#List Of Supported Hardware
List of devices goes here


#Widgets
### Common Widget Settings
Most of the settings are self-explainable, but there are some hidden features that you can use 

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


Notifications:
### Twitter

Twitter Widget connects your Twitter account to Blynk and allows you to send Tweets from your hardware. 

<img src="http://static1.squarespace.com/static/54765ba7e4b0d055ee0b47a6/54e92d39e4b0c31341b33a9a/55813d09e4b0ba8aa77ab230/1434533129525/TwitterON.png"/>


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
All the commands you can use in code
### Virtual_Write
### Virtual_Read
### BLYNK_Print
### BLYNK_LOG
### BLYNK_CONNECT
### 


#Blynk API. Writing your own library
Instructions on how to add support for new hardware 

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
