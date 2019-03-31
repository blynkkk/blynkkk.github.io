#FAQ

- I backed Blynk on Kickstarter. Where are my widgets and why the app is free?
> App is free because otherwise you would have to pay to download it. This is how AppStore and Google Play works.
> Current Blynk release has a limited amount of widgets. We decided to make them free for everyone until we implement store. After that, every widget will be paid. However every backer will get them for free (according to their pledge).
  
- What is Blynk Cloud?
> Blynk Cloud is a open-source software written on Java using plain TCP/IP and secured TCP/IP (for hardware that supports it) sockets and running on our server. Blynk iOS and Android apps connect to Blynk Cloud by default. Access is free for every Blynk user. We also provide a Private Server distribution for those who want to [install it locally](/#blynk-server).

- How much access to Cloud Blynk Server cost?
> It is free for every Blynk user.

- Can I run Blynk server locally?
> Yes. Those of you, who want extra security or don’t have internet connection, can install Local Blynk Server and run it in your own local network. Blynk Server is Open-Source and it takes less than few seconds to deploy. All the instructions and files are [here](/#blynk-server).

- What are the requirements to run Private Blynk Server?
> To run Private Blynk Server, all you need is Java Runtime Environment.

- Can I run Blynk server on Raspberry Pi?
> Yes, surely! [Here is instruction](/#blynk-server-how-to-run-local-blynk-server-launch-blynk-server-on-raspberry-pi).

- Does Blynk app work over Bluetooth?
> Yes. It is in beta right now.

- Does Blynk support Ethernet / Wi-FI / UART?
> Yes, all of them. See full list of [supported hardware](/#supported-hardware) and shields.

- I don't have any shield. Can I use Blynk with my computer?
> Yes, you can use Blynk just with a USB cable. There is a step-by-step [instruction](/#other-hardware-connect-over-usb) on how to do it.

- Can Blynk handle multiple Arduinos?
> Yes. There 3 ways right now :
> - add multiple devices to your project.
> - you may use same [Auth Token](/#getting-started-getting-started-with-application-auth-token) for different hardware. In that case you can control few hardwares from 1 dashboard.
> - you can do it using [Bridge functionality](/#widgets-other-bridge) which allows you to send messages from one hardware to another.

- Does Blynk server store sensor data when app goes offline?
> Yes, every command that hardware sends to server is stored. You could use [History Graph](/#widgets-displays-superchart) widget in order to view it.

- How many Virtual Pins I can use?
> It depends mostly on your hardware. Low-end hardware may use up to 32 Virtual Pins. More powerful (like ESP8266) can 
> use up to 128 but it requires also BLYNK_USE_128_VPINS property in your sketch. [Example](https://github.com/blynkkk/blynk-library/blob/master/src/Blynk/BlynkConfig.h#L64).

- Why app requires all this permissions?
> http://help.blynk.cc/faq/blynk-android-permissions-explained