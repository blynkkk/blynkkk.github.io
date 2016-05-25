#Supported Hardware

## Platforms

- **Arduino** (https://github.com/blynkkk/blynk-library)
  - Arduino Uno, Duemilanove
  - Arduino Nano, Mini, Pro Mini, Pro Micro, Due, Mega
  - Arduino 101 (Intel Curie)
  - Arduino MKR1000
  - Arduino Zero
  - Arduino Yún (onboard WiFi and Ethernet, via Bridge)
- **Arduino-like**
  - Generic ESP8266, NodeMCU, Huzzah, WeMos D1, Seeed Wio Link, etc.
  - Intel Edison
  - Intel Galileo
  - Teensy 3.2/3.1
  - RedBearLab Blend Micro
  - LightBlue Bean *, soon*
  - Simblee BLE *, soon*
  - LinkIt ONE
  - TinyCircuits TinyDuino (CC3000)
  - Microduino/mCookie Core, Core+, CoreUSB
  - Wicked WildFire V3 (CC3000)
  - Oak by Digistump
  - chipKIT Uno32
- **Energia**
  - Texas Instruments
    - CC3200-LaunchXL
    - Tiva C Connected LaunchPad
    - Stellaris LM4F120 LaunchPad
  - RedBearLab (CC3200, WiFi Mini)
- **Particle** (formerly Spark: https://github.com/vshymanskyy/blynk-library-spark)
  - Core
  - Photon
  - Electron
  - RedBear Duo
- **ARM mbed** (soon)
  - Seeed Tiny BLE
  - RedBearLab BLE Nano
  - BBC Micro:bit
- **JavaScript** (Node.js, Espruino, Browser) (https://www.npmjs.com/package/blynk-library)
  - Regular PC with Linux / Windows / OS X
  - Raspberry Pi (Banana Pi, Orange Pi, ...)
  - BeagleBone Black
  - PandaBoard
  - CubieBoard
  - pcDuino
  - Tessel 2
  - Intel Edison
  - Intel Galileo
  - VoCore (OpenWRT + [Espruino package](https://github.com/vshymanskyy/OpenWRT-Espruino-packages))
  - Espruino Pico
  - ...
- **Python** (MicroPython)
  - WiPy

## Arduino connection types

- USB (Serial), connected to your laptop or desktop
- Arduino Ethernet Shield 2 (W5500)
- Arduino Ethernet Shield (W5100)
- Arduino WiFi 101 Shield
- Arduino WiFi Shield
- Adafruit Bluefruit LE (nRF8001 Breakout, BLE 4.0)
- HM-10, HC-08 Bluetooth Low Energy modules
- Adafruit CC3000 WiFi Breakout / Shield
- ENC28J60 - based boards
- ESP8266 as WiFi modem (running original firmware)
- SeeedStudio Ethernet Shield V2.0 (W5200)
- RN-XV WiFly
- You can implement your own connection type easily (see [this](https://github.com/blynkkk/blynk-library/blob/master/examples/BoardsAndShields/User_Defined_Connection/User_Defined_Connection.ino) example)!

## Made by Community

- [WIZnet-W5500-EVB](http://instructables.com/id/WIZnet-W5500-EVB-and-Blynk-App-communication)
- [LabVIEW](https://github.com/juncaofish/NI-LabVIEWInterfaceforBlynk)
- [Node-RED](https://github.com/tzapu/node-red-contrib-blynk) (can be used as bridge to HTTP, TCP, UDP, MQTT, XMPP, IRC, OSC...)
