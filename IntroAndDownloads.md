<span style="color:#D3435C;">**NOTE:** This guide is a **Work In Progress**. You're welcome to use it, but please be aware that there might be mistakes, misspellings, broken links and some TODO items listed.</span>

#Intro
This guide will help you to understand how to get started using Blynk and give you the most comprehensive overview of all the features.
 
If you want to jump straight into playing with Blynk, check out Getting Started.
<br>

[Getting Started >](http://docs.blynk.cc/#getting-started)

##How Blynk Works
Blynk was designed for the Internet of Things. It can control hardware remotely, it can display sensor data, 
it can store data, analyze and do many other cool things. 

There are three major components in the platform: 

- **Blynk App** - allows to you create amazing interfaces for your projects using various widgets we provide.

- **Blynk Server** - responsible for all the communications between the smartphone and hardware. 
You can use our Blynk Cloud or run your [private Blynk server](http://docs.blynk.cc/#blynk-server-requirements) locally. 
It's open-source, could easily handle thousands of devices and can even be launched on a Raspberry Pi.

- **Blynk Libraries** - for all the popular hardware platforms - enable communication with the server and 
process all the incoming and outcoming commands.

Now imagine: every time you press a Button in the Blynk app, the message travels to ~~space~~ the Blynk Cloud, 
where it magically finds its way to your hardware. It works the same in the opposite direction and 
everything happens in a *blynk* of an eye.

<img src="images/architecture.png" style="width: 640px; height:478px"/>

##What do I need to Blynk?
At this point you might be thinking: **"Ok, I want it. What do I need to get started?"** – Just a couple of things, really:

####**Hardware**. 
An Arduino, Raspberry Pi, or a similar development kit.

**Blynk works over the Internet.** 
This means that the hardware you choose should be able to connect to over the internet. Some of the boards, like Arduino Uno 
will need an Ethernet or Wi-Fi Shield to communicate, others are already Internet-enabled: like the ESP8266, Raspberri Pi, 
Particle Photon or SparkFun ESP Thing. But even if you don't have a shield, you can connect over USB to your 
laptop or desktop (it's a bit more complicated for newbies, but we got you covered). 
What's cool, is that the [list of hardware](http://docs.blynk.cc/#list-of-supported-hardware) that works with Blynk is huge and will keep on growing. 
  
####**A Smartphone**. 
The Blynk App is a well designed interface builder. It works on both iOS and Android, so no holywars here, ok? 

#Downloads
##**Blynk Apps for iOS or Android** <br> 
[<img src="http://static1.squarespace.com/static/54765ba7e4b0d055ee0b47a6/t/55515fd0e4b08237a78598e2/1431396305454/?format=500w" alt="Drawing" style=" width: 150px; height:53px"/>](https://itunes.apple.com/us/app/blynk-control-arduino-raspberry/id808760481?ls=1&mt=8)  &nbsp; &nbsp; &nbsp; &nbsp;[<img src="http://static1.squarespace.com/static/54765ba7e4b0d055ee0b47a6/t/55515fe8e4b08237a785995e/1431396357648/?format=750w" alt="Drawing" style=" width: 200px; height:53px"/>](https://play.google.com/store/apps/details?id=cc.blynk)

##**Blynk Library** <br>
[Download The Blynk Library >](https://github.com/blynkkk/blynk-library/releases/latest)

In case you forgot how to or don't know how to install Arduino libraries [click here](http://www.arduino.cc/en/guide/libraries).
