# Supported Hardware

Blynk supports more than 400 boards already, including support for Arduino, Particle, ARM mbed, TI Energia, MicroPython, Node.js, OpenWRT and many Single Board Computers. You can add your own connection types easily (see [these](https://github.com/blynkkk/blynk-library/tree/master/examples/More/ArduinoClient) examples for Arduino)!

## Platforms

- **Arduino** (https://github.com/blynkkk/blynk-library)
  - Arduino Uno, Duemilanove
  - Arduino Nano, Mini, Pro Mini, Pro Micro, Due, Mega
  - Arduino 101 (Intel Curie, with BLE)
  - Arduino MKR1000
  - Arduino Zero
  - Arduino Yún (onboard WiFi and Ethernet, via Bridge)
  
- **Arduino-like**
  - Blynk Board
  - ESP8266 (Generic, NodeMCU, Witty Cloud, Huzzah, WeMos D1, Seeed Wio Link, etc.)
  - ESP32 Dev Board
  - nRF51/nRF52 - based boards
  - Teensy 3.2/3.1
  - Blue Pill (STM32F103C)
  - BBC micro:bit
  - LightBlue Bean *, soon*
  - DFRobot Bluno
  - RedBear Duo (WiFi, BLE)
  - RedBearLab Blend Micro
  - RedBearLab BLE Nano (v1 and v2)
  - Seeed Tiny BLE
  - Simblee BLE
  - RFduino BLE
  - The AirBoard (BLE-Link, RN-XV)
  - Feather M0 WiFi
  - Feather 32u4 BLE
  - Intel Edison
  - Intel Galileo
  - Fishino Guppy, Uno, Mega
  - TinyCircuits TinyDuino (CC3000)
  - Microduino/mCookie Core, Core+, CoreUSB
  - Wicked WildFire V2, V3, V4
  - Digistump Oak
  - chipKIT Uno32
  - Alorium XLR8 (FPGA)
  - LinkIt ONE (WiFi only)
- **Energia**
  - Texas Instruments
    - CC3200-LaunchXL
    - Tiva C Connected LaunchPad
    - Stellaris LM4F120 LaunchPad
    - MSP430F5529 + CC3100
    - LaunchPad MSP432
  - RedBearLab (CC3200, WiFi Mini)

- **Particle** https://github.com/vshymanskyy/blynk-library-spark)
  - Core
  - Photon
  - Electron
  - RPi
  - SparkFun RedBoard
  - RedBear Duo (WiFi & BLE)

- **ARM mbed** (https://developer.mbed.org/users/vshymanskyy/code/Blynk/)
  - Seeed Tiny BLE
  - RedBearLab BLE Nano
  - BBC micro:bit
  - STM32 Nucleo + Wiznet 5100 *, soon*

- **JavaScript** (Node.js, Espruino, Browsers) (https://www.npmjs.com/package/blynk-library)
  - Regular PC with Linux / Windows / OS X
  - Raspberry Pi (Banana Pi, Orange Pi, ...)
  - BeagleBone Black
  - Onion Omega
  - Intel Galileo
  - Intel Edison
  - Intel Joule
  - LeMaker Guitar
  - LeMaker Banana Pro
  - Samsung ARTIK 5
  - PandaBoard, CubieBoard, pcDuino, Tessel 2
  - VoCore (OpenWRT + [Espruino package](https://github.com/vshymanskyy/OpenWRT-Espruino-packages))
  - Espruino Pico
  - ...

- **Python** (https://github.com/vshymanskyy/blynk-library-python)
  - MicroPython
  - Python 2
  - Python 3

- **Lua** (https://github.com/blezek/blynk-esp)
  - NodeMCU

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
  - DFRobot BLE-Link module
  - Microduino/mCookie BLE
  - RedBearLab BLE Mini
  - nRF8001-based boards (Adafruit Bluefruit LE, etc.)
 
- **Bluetooth 2.0 Serial Port Profile (SPP)**
  - HC-05, HC-06, ...
 
- **GSM/3G:**
  - SIMCom SIM800 series (SIM800A, SIM800C, SIM800L, SIM800H, SIM808, SIM868)
  - SIMCom SIM900 series (SIM900A, SIM900D, SIM908, SIM968)
  - A6/A7
  - M590 *(beta)*
  - GPRSbee
  - Microduino GSM
  - Adafruit FONA (Mini Cellular GSM Breakout)
  - Adafruit FONA 800/808 Shield

## Made by Community

- [WIZnet-W5500-EVB](http://instructables.com/id/WIZnet-W5500-EVB-and-Blynk-App-communication)
- [LabVIEW](https://github.com/juncaofish/NI-LabVIEWInterfaceforBlynk)
- [Node-RED](https://github.com/tzapu/node-red-contrib-blynk) (can be used as bridge to HTTP, TCP, UDP, MQTT, XMPP, IRC, OSC...)

## Boards known to have problems

These boards are not supported and seem not work out of the box:
- [Arduino UNO WiFi](http://www.arduino.org/products/boards/arduino-uno-wifi)
- [Arduino Tian](http://www.arduino.org/products/boards/arduino-tian)
