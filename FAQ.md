#FAQ

- I backed Blynk on Kickstarter. Where are my widgets and why the app is free?
> App is free becasuse otherwise you would have to pay to download it. This is how AppStore and Google Play works.
> Current Blynk release has a limited amount of widgets. We decided to make them free for everyone until we implement store. After that, every widget will be paid. However every backer will get them for free (according to their pledge).
  
- What is Blynk Cloud?
> Blynk Cloud is a open-source software written on Java using plain TCP/IP and secured TCP/IP (for hardware that supports it) sockets and running on our server. Blynk iOS and Android apps connect to Blynk Cloud by default. Access is free for every Blynk user. We also provide a Private Server distribution for those who want to install it locally. All the instructions and files are on [our Github page](https://github.com/blynkkk/blynk-server).

- How much access to Cloud Blynk Server cost?
> It is free for every Blynk user.

- Can I run Blynk server locally?
> Yes. Those of you, who want extra security or don’t have internet connection, can install Local Blynk Server and run it in your own local network. Blynk Server is Open-Source and it takes less than few seconds to deploy. All the instructions and files are on [our Github page](https://github.com/blynkkk/blynk-server#blynk-server).

- What are the requirements to run Private Blynk Server?
> To run Private Blynk Server, all you need is Java Runtime Environment.

- Can I run Blynk server on Raspberry Pi?
> Yes, surely! [Here is instruction](https://github.com/blynkkk/blynk-server#quick-local-server-setup-on-raspberry-pi).

- Does Blynk app work over Bluetooth?
> No. But it's planned for next releases.

- Does Blynk support Ethernet / Wi-FI / UART?
> Yes, all of them. See full list of [supported hardware](http://blynkkk.github.io/#list-of-supported-hardware) and shields.

- I don't have any shield. Can I use Blynk with my computer?
> Yes, you can use Blynk just with a USB cable. There is a step-by-step [instruction](http://blynkkk.github.io/#other-hardware-connect-over-usb) on how to do it.

- Can Blynk handle multiple Arduinos?
> Yes. There 2 ways right now :
> - you may use same [Auth Token](http://blynkkk.github.io/#getting-started-getting-started-with-application-auth-token) for different hardware. In that case you can control few hardwares from 1 dashboard.
> - you can do it using [Bridge functionality](http://blynkkk.github.io/#widgets-other-bridge) which allows you to send messages from one hardware to another.

- Does Blynk server store sensor data when app goes offline?
> Yes, for all push widgets. We also plan to implement Data Log Widget, which will show you historical data on an app.
