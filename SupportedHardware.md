#Supported Hardware

## Platforms

- **Arduino** (https://github.com/blynkkk/blynk-library)
  - Uno, Duemilanove (select "UNO" in the list, not the "Due")
  - Nano, Mini, Pro Mini, Pro Micro
  - Mega
  - YÚN (onboard WiFi and Ethernet, via Bridge)
  - Due - limited support
- **Arduino-like**
  - ESP8266 (running standalone, using https://github.com/esp8266/Arduino)
  - Intel Edison
  - Intel Galileo
  - LinkIt ONE
  - Wicked WildFire (CC3000)
  - TinyCircuits TinyDuino (CC3000)
  - LightBlue Bean *, soon*
- **Energia**
  - Texas Instruments
    - CC3200-LaunchXL
    - Tiva C Connected LaunchPad
    - Stellaris LM4F120 LaunchPad
  - RedBearLab (CC3200, WiFi Mini)
- **Particle** (formerly Spark: https://github.com/vshymanskyy/blynk-library-spark)
  - Core
  - Photon
- **ARM mbed** (soon)
  - Seeed Tiny BLE
  - RedBearLab BLE Nano
  - BBC Micro:bit
- **JavaScript** (Node.js, Espruino) (https://www.npmjs.com/package/blynk-library)
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
- Official Ethernet shield (W5100)
- Official Arduino WiFi shield
- Adafruit Bluefruit LE (nRF8001 Breakout, BLE 4.0) *, soon*
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
