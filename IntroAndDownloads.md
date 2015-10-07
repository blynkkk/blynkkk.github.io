<span style="color:#D3435C;">**NOTE:** This page is a "Work In Progress". So there might be mistakes, misprints, broken links and some TODO items listed. You are welcome to use it, just be aware of that.</span>

#Intro
This guide will help you to understand how to get started using Blynk and give you the most comprehensive overview of all the features.
 
If you want to jump straight into playing with Blynk, check out Getting Started.
<br>

[Getting Started >](http://docs.blynk.cc/#getting-started)

##How Blynk Works
Blynk was designed for the Internet of Things. It can control hardware remotely, it can display sensor data and do lot's of other cool things with electronics. 

There are three major components in the platform: 

- **Blynk Apps** – allow to you create amazing interfaces for the projects from various Widgets we provide.

- **Blynk Server** is responsible for all the communications between the smartphone and hardware. You can use our Blynk Cloud or run your [private Blynk server](http://docs.blynk.cc/#blynk-server-requirements) locally. It's open-source and can be launched even on Raspberry Pi.

- **Blynk Libraries** for all the popular hardware platforms - enable communication with the server and process all the incoming and outcoming commands.

Now imagine: every time you press a Button in the Blynk app, the message travels to ~~space~~ Blynk Cloud, where it magically finds the way to your hardware. It works the same in the opposite direction and everything happens in a blynk of an eye.

<img src="images/architecture.png" style="width: 640px;"/>

##What do I need to Blynk?
At this point you might be thinking: **"Ok, I want it. What do I need to start?"** – Just a couple of things, really:

####**Hardware**. 
We hope you already have an Arduino or someting similar. If not - come on, get one ASAP!

**Blynk works over the Internet.** 
It means that the hardware you choose should be able to connect to Internet. Some of the boards, like Arduino Uno will need an Ethernet or Wi-Fi Shield to communicate, 
others are already Internet-enabled: like ESP8266, Particle Photon or SparkFun ESP Thing. But even if you don't have a shield, 
you can connect over the USB to your laptop or desktop (it's a bit more complicated for newbie, but we got you covered). 
What's cool, is that the [list of hardware](http://docs.blynk.cc/#list-of-supported-hardware) that works with Blynk is really huge. 
  
####**A Smartphone**. 
Blynk App is a well-designed interface builder. It works on both iOS and Android, so no holywars here, ok? 

#Downloads
##**Blynk Apps for iOS or Android** <br> 
[<img src="http://static1.squarespace.com/static/54765ba7e4b0d055ee0b47a6/t/55515fd0e4b08237a78598e2/1431396305454/?format=500w" alt="Drawing" style=" width: 150px;"/>](https://itunes.apple.com/us/app/blynk-control-arduino-raspberry/id808760481?ls=1&mt=8)  &nbsp; &nbsp; &nbsp; &nbsp;[<img src="http://static1.squarespace.com/static/54765ba7e4b0d055ee0b47a6/t/55515fe8e4b08237a785995e/1431396357648/?format=750w" alt="Drawing" style=" width: 200px;"/>](https://play.google.com/store/apps/details?id=cc.blynk)

##**Blynk Library** <br>
[Download Blynk Library >](https://github.com/blynkkk/blynk-library/releases/latest)

In case you don't know, or forgot how to install Arduino libraries [check here](http://www.arduino.cc/en/guide/libraries).
