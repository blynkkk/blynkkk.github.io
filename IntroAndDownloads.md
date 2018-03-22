#Intro
This guide will help you understand how to get started using Blynk and give a comprehensive overview of all the features.
 
If you want to jump straight into playing with Blynk, check out Getting Started.
<br>

[Getting Started >](http://docs.blynk.cc/#getting-started)

##How Blynk Works
Blynk was designed for the Internet of Things. It can control hardware remotely, it can display sensor data, 
it can store data, vizualize it and do many other cool things. 

There are three major components in the platform: 

- **Blynk App** - allows to you create amazing interfaces for your projects using various widgets we provide.

- **Blynk Server** - responsible for all the communications between the smartphone and hardware. 
You can use our Blynk Cloud or run your [private Blynk server](http://docs.blynk.cc/#blynk-server) locally. 
It's open-source, could easily handle thousands of devices and can even be launched on a Raspberry Pi.

- **Blynk Libraries** - for all the popular hardware platforms - enable communication with the server and 
process all the incoming and outcoming commands.

Now imagine: every time you press a Button in the Blynk app, the message travels to ~~space~~ the Blynk Cloud, 
where it magically finds its way to your hardware. It works the same in the opposite direction and 
everything happens in a blynk of an eye.

<img src="https://d1bhbfzxsgnz1o.cloudfront.net/images/architecture.png" style="width: 640px; height:478px"/>

##Features
* Similar API & UI for all supported hardware & devices
* Connection to the cloud using:
  * WiFi
  * Bluetooth and BLE
  * Ethernet
  * USB (Serial)
  * GSM
  * ...
* Set of easy-to-use Widgets
* Direct pin manipulation with no code writing
* Easy to integrate and add new functionality using virtual pins
* History data monitoring via History Graph widget
* Device-to-Device communication using Bridge Widget
* Sending emails, tweets, push notifications, etc.
* ... new features are constantly added!

You can find [example sketches](https://github.com/blynkkk/blynk-library/tree/master/examples) covering basic Blynk Features. 
They are included in the library. All the sketches are designed to be easily combined with each other.

##What do I need to Blynk?
At this point you might be thinking: **"Ok, I want it. What do I need to get started?"** – Just a couple of things, really:

####**1. Hardware**. 
An Arduino, Raspberry Pi, or a similar development kit.

**Blynk works over the Internet.** 
This means that the hardware you choose should be able to connect to the internet. Some of the boards, like Arduino Uno 
will need an Ethernet or Wi-Fi Shield to communicate, others are already Internet-enabled: like the ESP8266, Raspberri Pi with WiFi dongle, Particle Photon or SparkFun Blynk Board. But even if you don't have a shield, you can connect it over USB to your 
laptop or desktop (it's a bit more complicated for newbies, but we got you covered). 
What's cool, is that the [list of hardware](http://docs.blynk.cc/#supported-hardware) that works with Blynk is huge and will keep on growing. 
  
####**2. A Smartphone**. 
The Blynk App is a well designed interface builder. It works on both iOS and Android, so no holywars here, ok? 

#Downloads
##**Blynk Apps for iOS or Android** <br> 
[<img src="https://d1bhbfzxsgnz1o.cloudfront.net/images/appstore-lrg.svg" alt="Drawing" style=" width: 158px; height:42"/>](https://itunes.apple.com/us/app/blynk-control-arduino-raspberry/id808760481?ls=1&mt=8)  &nbsp; &nbsp; &nbsp; &nbsp;[<img src="https://play.google.com/intl/en_us/badges/images/apps/en-play-badge.png" alt="Drawing" style=" width: 158px; height:42px"/>](https://play.google.com/store/apps/details?id=cc.blynk)

##**Blynk Library** <br>
[Download The Blynk Library >](https://github.com/blynkkk/blynk-library/releases/latest)

In case you forgot, or don't know how to install Arduino libraries [click here](http://www.arduino.cc/en/guide/libraries).
