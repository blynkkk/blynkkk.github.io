#Getting Started  
Let's try to get you started in 5 minutes (reading doesn't counts!). 
We will try to switch an LED connected to your Arduino with the Smartphone.

Connect an LED as shown here:

<img src="images/Arduino_LED.jpg" style="width: 250px;"/>

##Getting started with application
###1. Create Blynk Account
After you download Blynk app, you'll need to create a new Blynk account. It's not connected to our Forum or Kickstarter - just create a New Account. 

Use a **real** e-mail address - it will be used later and you'll appreciate that.

<img src="images/sign_up.png" style="width: 200px;"/>

####Why do I need to create account?

Account is needed to store your Projects and for you to have access to them from multiple devices. It's also a security measure. 

You can always install your [Private Blynk Server](http://blynkkk.github.io/#blynk-server-requirements) and have full control.   

###2. Create new project
After you successfully logged into your account, start by creating a new Project. Give it a name.

<img src="images/create_new_project.png" style="width: 200px;"/>

###3. Choose your hardware
Select the hardware you will use. Check out how big is the [list of supported hardware](http://blynkkk.github.io/#list-of-supported-hardware)!

<img src="images/select_hardware.png" style="width: 200px;"/>

###4. Auth Token

**Auth Token** is a uniqie identifier which is needed to connect your Arduino or other board to your smartphone. Every new project you create will have an Auth Token.

<img src="images/token.png" style="width: 200px;"/>

<span style="color:#D3435C;">**NOTE:** Don't share your Auth Token with anyone, unless you want them to have access to your hardware. </span>

It's very convenient to send it over E-mail. Press E-mail button and token will be sent to the e-mail address you used for registration. 
You can also tap on the Token itself and it will be copied to the clipboard.

Now press **"Create"** button.  

<img src="images/new_project.png" style="width: 200px;"/>

###5. Add a Widget

Your project is empty, so let's add a Button to control our LED.

Tap anywhere on empty space - Whoa! you got inside a Widget Box! All the widgets are here. Now pick a Button.

**Widget Box**

<img src="images/widgets_box.png" style="width: 200px;"/>

<img src="images/project_with_button.png" style="width: 200px;"/>

**Drag-n-Drop**
Tap and hold the Widget to drag it to teh new position.

**Widget Settings**
Each Widget has it's own settings. Tap on the widget to get to them

<img src="images/button_settings.png" style="width: 200px;"/>

The most important parameter to set is **PIN** . List of pins reflects physical pins defined by your hardware. If your LED is connected to Digital Pin 8 - then select **D8** (**D** - stands for **D**igital).    

<img src="images/pin_selection.png" style="width: 200px;"/>

###6. Run the project
When you are done with the Settings - press **PLAY** button. This will switch you from EDIT mode to PLAY mode where you can interact with the hardware. Now you can't drag or set up Widgets, but if you need it: press **STOP** and get back to Edit Mode.

<img src="images/play_button.png" style="width: 200px;"/>

You may get a message "Arduino UNO is offline". Don't worry now. We'll get to that in a minute.

##Getting started with hardware
Hope you have Blynk Library installed. If not - [check here](http://blynkkk.github.io/#downloads-blynk-library).

We've prepared example sketches that will get your microcomputer online. Open the example sketch according to the device or shield you are using.

<img src="images/connection_type_sketch.png" style="width: 500px;"/>

###How to use example sketches
Let's take a look at the simple sketch for [Arduino UNO + Ethernet shield](https://github.com/blynkkk/blynk-library/blob/master/examples/GettingStarted/BlynkBlink/BlynkBlink.ino)

```cpp
#define BLYNK_PRINT Serial
#include <SPI.h>
#include <Ethernet.h>
#include <BlynkSimpleEthernet.h>

char auth[] = "YourAuthToken";

void setup()
{
  Serial.begin(9600); // See the connection status in Serial Monitor
  Blynk.begin(auth);  // Here your Arduino connects to the Blynk Cloud.
}

void loop()
{
  Blynk.run(); // All the Blynk Magic happens here...
}
```

###Auth Token
In this sketch find this line:

```cpp
char auth[] = "YourAuthToken";
```
This is the [Auth Token](http://blynkkk.github.io/#getting-started-getting-started-with-application-4-auth-token) that you've sent over e-mail recently. 
Please check your email - it should be there already. 
Copy it from e-mail and put inside curly brackets. 

``` 
char auth[] = "f45626c103a94983b469637978b0c78a";
``` 

Upload sketch to the board and open Serial Terminal. Wait until you see something like this: 

``` 
Blynk v.1.0.3
Your IP is 192.168.0.11
Connecting...
Blynk connected!
```

<span style="color:#24C48C" >**Congrats! You are all set! Now your Arduino is connected to Blynk Cloud!**</span>

##Blynking
Go back to the Blynk app.
Push the Button and turn the LED On and Off!

<img src="images/button_pressed.png" style="width: 200px;"/>

Check out [other example sketches](https://github.com/blynkkk/blynk-library/tree/master/examples)! Always feel free to experiment and combine different examples together! 

For example, attach an LED to [PWM](http://www.arduino.cc/en/Tutorial/Fading)-enabled Pin on your Arduino. Set the Slider Widget to control brightness of an LED. Just use the same steps described above.
