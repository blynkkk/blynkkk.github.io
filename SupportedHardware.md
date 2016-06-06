#Supported Hardware

## Platforms

- **Arduino** (https://github.com/blynkkk/blynk-library)
  - Arduino Uno, Duemilanove
  - Arduino Nano, Mini, Pro Mini, Pro Micro, Due, Mega
  - Arduino 101 (Intel Curie, with BLE)
  - Arduino MKR1000 (WiFi)
  - Arduino Zero
  - Arduino Yún (onboard WiFi and Ethernet, via Bridge)
- **Arduino-like**
  - Blynk Board
  - Generic ESP8266, NodeMCU, Huzzah, WeMos D1, Seeed Wio Link, etc.
  - Intel Edison
  - Intel Galileo
  - Teensy 3.2/3.1
  - RedBearLab Blend Micro
  - LightBlue Bean *, soon*
  - Simblee BLE
  - LinkIt ONE (WiFi only)
  - TinyCircuits TinyDuino (CC3000)
  - Microduino/mCookie Core, Core+, CoreUSB
  - Wicked WildFire V2, V3, V4
  - Digistump Oak
  - chipKIT Uno32
  - Alorium XLR8 (FPGA)
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
  - SparkFun RedBoard
  - RedBear Duo (WiFi & BLE)
- **ARM mbed** *soon*
  - Seeed Tiny BLE
  - RedBearLab BLE Nano
  - BBC Micro:bit
  - STM32 Nucleo + Wiznet 5100 *, soon*
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
- **Ethernet:**
 - Arduino Ethernet Shield (W5100)
 - Arduino Ethernet Shield 2 (W5500)
 - SeeedStudio Ethernet Shield V2.0 (W5200)
 - ENC28J60-based modules
- **WiFi:**
 - ESP8266 as WiFi modem (running original firmware)
 - Arduino WiFi 101 Shield
 - Arduino WiFi Shield
 - Adafruit CC3000 WiFi Breakout / Shield
 - RN-XV WiFly
- **Bluetooth Smart (BLE 4.0):**
 - HM-10, HC-08
 - RedBearLab BLE Mini
 - nRF8001-based boards (Adafruit Bluefruit LE, etc.)
- **GSM/3G:**
 - SIM800 *, soon*
- You can implement your own connection type easily (see [this](https://github.com/blynkkk/blynk-library/blob/master/examples/Boards_USB_Serial/User_Defined_Connection/User_Defined_Connection.ino) example)!

## Made by Community

- [WIZnet-W5500-EVB](http://instructables.com/id/WIZnet-W5500-EVB-and-Blynk-App-communication)
- [LabVIEW](https://github.com/juncaofish/NI-LabVIEWInterfaceforBlynk)
- [Node-RED](https://github.com/tzapu/node-red-contrib-blynk) (can be used as bridge to HTTP, TCP, UDP, MQTT, XMPP, IRC, OSC...)
