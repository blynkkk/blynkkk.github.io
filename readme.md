#Getting Started


###Download all the ingridients
**Blynk App for iOS or Android:** <br> <br>
[App Store >](https://itunes.apple.com/us/app/blynk-control-arduino-raspberry/id808760481?ls=1&mt=8)[Google Play >](https://play.google.com/store/apps/details?id=cc.blynk) 


**Install Blynk Library:** <br><br>
[Download Blynk Library >](https://github.com/blynkkk/blynk-library/archive/v0.2.1.zip)

In case you forgot how to install Arduino libraries: check [here](http://www.arduino.cc/en/guide/libraries).  We are also good friends of **[codebender](https://codebender.cc/example/BlynkSimpleEthernet/GettingStarted:BlynkBlink)** - you can upload Blynk sketches directly from your browser

###Wire everything 
Use this wiring scheme to connect LED to your Hardware.


<img src="http://faberfun.com/wp-content/uploads/2013/08/Blink-LED-using-Arduino-uno.jpg" alt="Drawing" style="width: 250px;"/>

### Create Blynk Account 
>Screenshot


### Get Auth Token
**Auth Token** is used to connect your Arduino or other board to your smartphone. Every new project you create will have an Auth Token. 

>Screenshot

It's very convenient to send it over E-mail. If you press E-mail button – token will be sent to the e-mail address you used for registration. If you have a good memory - you can memorize it ;) or tap the number and it will be copied to the clipboard.

### Choose your hardware
Select the hardware that will be used for your project. Yes, this list is long.


>Screenshot



#Let's get online
You know that **Blynk works over the Internet**, right? (BTW, Bluetooth LE is on the way) 

Blynk works with almost anything, check the [full list of supported hardware]()

Before you start Blynking, you need to understand how you will connect to the Internet. May be it's an Ethernet Shield for Arduino, or may be your hardware is already internet-enabled (e.g. Spark Core). 

We've prepared sketches that will get your microcomputer online. Open the example sketch according to your device or shield. If you are using **codebender** - find the example in the list

> Screenshot

Find next line in the code:

``` 
char auth[] = "YourAuthToken";

```

Change it by putting your Auth Token inside curly brackets:

``` 
char auth[] = "123456789abcdefghijk0987654321";

```

Upload sketch to the board and open Serial Terminal. Wait until you see something like this: 

``` 
Your IP is 192.168.0.11
Connecting...
Blynk connected!

```
**Congratulations! You are all set to Blynk!**

###Connect over USB,  and others

* You can play with Blynk directly over USB. It's a bit tricky for newbies, but if you follow these [USB instructions](link) you'll succeed for sure.

###Raspberry Pi, Spark Core
* **Spark Core** owners: check [here]()
* **Raspberry Pi** eaters: [here]() 


# Setting up your first Blynk project

Open your project in the app. It's empty now, so let's add a Button. Just tap anywhere on empty space - Widget Box will open. Choose the Button Widget.

> Screenshot

Hold and drag it to reposition

> Screenshot

Tap on the widget to get to it's settings  

> Screenshot


___

### Quickstart: Arduino + Ethernet shield

* Download the Blynk app ([App Store](https://itunes.apple.com/us/app/blynk-control-arduino-raspberry/id808760481?ls=1&mt=8), [Google Play](https://play.google.com/store/apps/details?id=cc.blynk)) 
* Get the Auth Token from the app
* Import this library to Arduino IDE. Guide [here](http://arduino.cc/en/guide/libraries)
* In Arduino IDE, select File -> Examples -> Blynk -> BoardsAndShields -> Arduino_Ethernet
* Update Auth Token in the sketch and upload it to Arduino
* Connect your Arduino with Ethernet shield to the internet

### Supported boards, WiFi, Serial, USB...

[See examples](examples/BoardsAndShields) with different connection types.

Full list of supported hardware is [here](http://community.blynk.cc/t/hardware-supported-by-blynk).

### Docs

* [Basics](./docs/Basics.md)
* [Widgets](./docs/Widgets.md)
* [Security](./docs/Security.md)
* [Platforms/Connection types](./docs/Platforms.md)
* [Troubleshooting](./docs/Troubleshooting.md)
* [Implementing your own library](./docs/Implementing.md)

### License

This project is released under The MIT License (MIT)


#Links

* [Kickstarter campaign](https://www.kickstarter.com/projects/167134865/blynk-build-an-app-for-your-arduino-project-in-5-m/description)
* [Blynk downloads, docs, tutorials](http://www.blynk.cc)
* [Blynk community](http://community.blynk.cc)
* [Facebook](http://www.fb.com/blynkapp)
* [Twitter](http://twitter.com/blynk_app)
