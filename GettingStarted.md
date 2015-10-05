#Getting Started
##Downloads
**Blynk App for iOS or Android:** <br> <br> 
[<img src="http://static1.squarespace.com/static/54765ba7e4b0d055ee0b47a6/t/55515fd0e4b08237a78598e2/1431396305454/?format=500w" alt="Drawing" style=" width: 150px;"/>](https://itunes.apple.com/us/app/blynk-control-arduino-raspberry/id808760481?ls=1&mt=8)  &nbsp; &nbsp; &nbsp; &nbsp;[<img src="http://static1.squarespace.com/static/54765ba7e4b0d055ee0b47a6/t/55515fe8e4b08237a785995e/1431396357648/?format=750w" alt="Drawing" style=" width: 200px;"/>](https://play.google.com/store/apps/details?id=cc.blynk)

**Install Blynk Library:** <br><br>
[Download Blynk Library >](https://github.com/blynkkk/blynk-library/releases/latest)

In case you forgot how to install Arduino libraries: check [here](http://www.arduino.cc/en/guide/libraries).  We are also good friends of **[codebender](https://codebender.cc/example/BlynkSimpleEthernet/GettingStarted:BlynkBlink)** - you can code and upload Blynk sketches to your hardware directly from your browser.

##Getting started with application

###1. Create new Blynk cccount
Account is needed to store your Projects and to have access from multiple devices.   

<img src="images/sign_up.png" style="width: 300px;"/>

###2. Create new project
After you successfully logged in to your account, start by creating a new Project. Give it a name.

<img src="images/new_project.png" style="width: 300px;"/>

###3. Choose your hardware
Select the hardware you are building project with.

<img src="images/select_hardware.png" style="width: 300px;"/>

###4. Send Auth Token

**Auth Token** is a uniqie identifier which is used to connect your Arduino or other board to your smartphone. Every new project you create will have an Auth Token.

It's very convenient to send it over E-mail. Press E-mail button – token will be sent to the e-mail address you used for registration. You can also tap on it and it will be copied to the clipboard

<span style="color:#D3435C;">**NOTE:** Don't share your Auth Token with anyone, unless you want them to have access to your hardware. </span>

Press **"Create"** button.  


<img src="images/new_project.png" style="width: 300px;"/>






##Getting started with hardware

You know that **Blynk works over the Internet**, right? (Bluetooth LE is on the way) 

Before you start Blynking, you need to understand how you will connect to the Internet. It can be an Ethernet Shield for Arduino, Wi-Fi or may be your hardware is already internet-enabled (e.g. Spark Core). 

We've prepared [example sketches](https://github.com/blynkkk/blynk-library/tree/master/examples/BoardsAndShields) which will get your microcomputer online. Open the example sketch according to your device or shield. If you are using **codebender** - find the example you need in the [list]().

<img src="images/connection_type_sketch.png" style="width: 500px;"/>

###Simplest sketch

[Simplest possible sketch](https://github.com/blynkkk/blynk-library/blob/master/examples/GettingStarted/BlynkBlink/BlynkBlink.ino) would be for Arduino UNO with Ethernet shield:

```cpp
#define BLYNK_PRINT Serial // Enables Serial Monitor
#include <SPI.h>
#include <Ethernet.h>
#include <BlynkSimpleEthernet.h> // This part is for Ethernet stuff

char auth[] = "YourAuthToken"; // Put your Auth Token here. (see Step 3 above)

void setup()
{
  Serial.begin(9600); // See the connection status in Serial Monitor
  Blynk.begin(auth);  // Here your Arduino connects to the Blynk Cloud.
}

void loop()
{
  Blynk.run(); // All the Blynk Magic happens here...

  // You can inject your own code or combine it with other sketches.
  // Check other examples on how to communicate with Blynk. Remember
  // to avoid delay() function!
}
```

###Insert auth token

In the example sketch find this line in code:


```cpp
char auth[] = "YourAuthToken";
```

Change it by putting your [Auth Token](http://blynkkk.github.io/#getting-started-getting-started-with-application-4-send-auth-token) inside curly brackets. 

```cpp 
char auth[] = "f45626c103a94983b469637978b0c78a";
``` 

Upload sketch to the board and open Serial Terminal. Wait until you see something like this: 

``` 
Your IP is 192.168.0.11
Connecting...
Blynk connected!
```

##Setup your project

Open your project in the app. It's empty now.

<img src="images/empty_project.png" style="width: 300px;"/>

So let's add a Button. Just tap anywhere on empty space - Widget Box will open. 

<img src="images/widgets_box.png" style="width: 300px;"/>

Choose the Button Widget.

<img src="images/project_with_button.png" style="width: 300px;"/>

Tap on the widget to get to it's settings  

<img src="images/button_settings.png" style="width: 300px;"/>

The most important parameter to set is **PIN** . List of pins reflects physical pins defined by your hardware. If your LED is connected to Digital Pin 8 - then select **D8** (**D** - stands for **D**igital).    

<img src="images/pin_selection.png" style="width: 300px;"/>

When you are done with the Settings - press **PLAY** button. This will switch you from EDIT mode to PLAY mode where you can interact with widgets.

<img src="images/play_button.png" style="width: 300px;"/>

Press Button to turn the LED On and Off

<img src="images/button_pressed.png" style="width: 300px;"/>

Always feel free to experiment! For example, attach an LED to [PWM](http://www.arduino.cc/en/Tutorial/Fading)-enabled Pin on your Arduino. Set the Slider Widget to control brightness of an LED. Just use the same steps described above.

<span style="color:#24C48C" >**Congratulations, that's it! Happy Blynking!**</span>