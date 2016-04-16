# Troubleshooting

## Connection

If you experience connection problems, follow these steps:

1. Check that your hardware, wires, cables and power supply are good quality, not harmed or damaged, etc.  
   Use high power USB cables and USB ports.
2. Check your wiring using the examples (TCP/HTTP Client or similar) **provided with your shield and hardware**.
   * Once you have some understanding how to configure connection, it's much easier to use Blynk.
3. Try running command ```telnet blynk-cloud.com 8442``` from your PC, connected to the same network as your board.
   You should see something like ```Connected to blynk-cloud.com.```.
4. Try running Blynk default examples for your platform **without modifications** to see if it is working.
   * Double-check that you have selected **the right example** for your connection type and board type.
   * Our examples come with **comments and explanations**. Read them carefully.
   * Check that your token is valid (copied from the App and **doesn't contain spaces, etc.**)
   * If it doesn't work, try looking into [serial debug prints](./Troubleshooting.md#enable-debug).
5. Done! Add your modifications and functionality. Enjoy Blynk!

***Note:*** when you have multiple devices connected to your network, they should all have different MAC and IP addresses. For example, when using 2 Arduino UNO with Ethernet shields, flashing default example to both of them will cause connection problems. You should use [manual ethernet configuration](https://github.com/blynkkk/blynk-library/blob/master/examples/BoardsAndShields/Arduino_Ethernet_Manual/Arduino_Ethernet_Manual.ino) example.

## WiFi network connection
If you encounter WiFi connection problems, please check these pitfalls:

* You're trying to connect to "WPA & WPA2 Enterprise" network (often used in offices), and your shield does not support this security method
* Your WiFi network has a login page that requests entering an access token (often used in restaurants)
* Your WiFi network security disallows connecting alien devices completely (MAC filtering, etc)

## Delay

Your application might be calling a delay() function or sleeps/cycles for a long time inside of the loop(), like this:

```cpp
void loop()
{
  ...
  delay(1000);
  other_long_operation();
  ...
  Blynk.run();
}
```
    
You should be aware that this can degrade performance of Blynk, or cause connection drops.

***Note:*** This also applies to the BLYNK_READ & BLYNK_WRITE handlers!

If you need periodic actions, consider using some timer library, like shown [in this example](https://github.com/blynkkk/blynk-library/blob/master/examples/GettingStarted/PushData/PushData.ino).

## Flood Error

If your code frequently sends a lot of requests to our server, your hardware will be disconnected. Blynk App may show "Your hardware is offline"

Here is an example of what may cause flood: ***DON'T DO THAT:***

When ```Blynk.virtualWrite``` is in the ```void loop```, it generates hundreds of "writes" per second 

```cpp
void loop()
{
  Blynk.virtualWrite(1, value);
  Blynk.run();
}
```

***SOLUTION:***
Send data in intervals. For example use SimpleTimer library, it's included in Blynk Library
Check [this example](https://github.com/blynkkk/blynk-library/blob/master/examples/GettingStarted/PushData/PushData.ino) to see how it can be done.

Using ```delay()``` will not solve the problem. It will create [another trouble](./Troubleshooting.md#delay). Use timers!


## Enable debug

To enable debug prints on the default Serial, add on the top of your sketch **(should be the first line
)**:

```cpp
#define BLYNK_DEBUG // Optional, this enables lots of prints
#define BLYNK_PRINT Serial
```
And enable serial in setup():

```cpp
Serial.begin(9600);
```

You can also use spare Hardware serial ports or SoftwareSerial for debug output (you will need an adapter to connect to it with your PC).

***Note:*** enabling debug mode will slowdown your hardware processing speed up to 10 times.
