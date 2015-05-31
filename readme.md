# Getting Started

###Download all the ingridients
**Blynk App for iOS or Android:** <br> <br>
[App Store >](https://itunes.apple.com/us/app/blynk-control-arduino-raspberry/id808760481?ls=1&mt=8)[Google Play >](https://play.google.com/store/apps/details?id=cc.blynk) 


**Install Blynk Library:** <br><br>
[Download Blynk Library >](https://github.com/blynkkk/blynk-library/archive/v0.2.1.zip)

In case you forgot how to install Arduino libraries: check [here] (http://www.arduino.cc/en/guide/libraries).  We are also good friends of **[codebender](https://codebender.cc/example/BlynkSimpleEthernet/GettingStarted:BlynkBlink)** - you can upload Blynk sketches directly from your browser

### Create Blynk Account 
>Screenshot

<br>

### Get Auth Token
**Auth Token** is used to connect your Arduino or other board to **Blynk Cloud** and then to your smartphone. Every new project you create will have an Auth Token. 

>Screenshot

It's very convenient to send it over E-mail. If you press E-mail button – token will be sent to the e-mail address you used when creating new account.




# Let's get you online
You know that **Blynk works over the Internet**, right? (BTW, Bluetooth LE is on the way) 

Before you start Blynking, you need to understand how you will connect to the Internet. May be it's an Ethernet Shield for Arduino, or may be your hardware is already internet-enabled (e.g. Spark Core). 

Blynk works with almost anything, please check the [full list of supported hardware]()

We've prepared lot's of example sketches. Choose your connection type and open the example sketch you need.

>Screenshot

You can also connect directly over USB. It's a bit more tricky, but if you follow these [USB instructions](link) you'll succeed for sure!


# Running Blynk



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
