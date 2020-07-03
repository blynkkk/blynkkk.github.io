# Hardware set-ups

## Arduino over USB \(no shield\)

If you don't have any shield and your hardware doesn't have any connectivity, you can still use Blynk – directly over USB :

1. Open [Arduino Serial USB example](https://github.com/blynkkk/blynk-library/blob/master/examples/Boards_USB_Serial/Arduino_Serial_USB/Arduino_Serial_USB.ino) and change [Auth Token](./#getting-started-getting-started-with-application-4-auth-token)

   ```cpp
    // You could use a spare Hardware Serial on boards that have it (like Mega)
    #include <SoftwareSerial.h>
    SoftwareSerial DebugSerial(2, 3); // RX, TX

    #define BLYNK_PRINT DebugSerial
    #include <BlynkSimpleStream.h>

    // You should get Auth Token in the Blynk App.
    // Go to the Project Settings (nut icon).
    char auth[] = "YourAuthToken";

    void setup()
    {
      // Debug console
      DebugSerial.begin(9600);

      // Blynk will work through Serial
      Serial.begin(9600);
      Blynk.begin(auth, Serial);
    }

    void loop()
    {
      Blynk.run();
    }
   ```

2. Run the script which is usually located in `/scripts` folder:
   * Windows:`My Documents\Arduino\libraries\Blynk\scripts`
   * Mac    `User$/Documents/Arduino/libraries/Blynk/scripts`

**On Windows:**

Open cmd.exe

Write your path to blynk-ser.bat folder. For example:

```text
cd C:\blynk-library-0.3.1\blynk-library-0.3.1\scripts
```

Run `blynk-ser.bat` file. For example : `blynk-ser.bat -c COM4` \(where COM4 is port with your Arduino\)

And press "Enter", press "Enter" and press "Enter"

**On Linux and Mac**:

Navigate to /scripts folder. For example:

```text
cd User$/Documents/Arduino/libraries/Blynk/scripts
```

When inside this folder, run:

```text
user:scripts User$ ./blynk-ser.sh
```

**Warning:** Do no close terminal window with running script.

In some cases you may also need to perform :

```text
user:scripts User$ chmod +x blynk-ser.sh
```

You may need also to run it with `sudo`

```text
user:scripts User$ sudo ./blynk-ser.sh
```

This is what you'll see in Terminal app on Mac \(usbmodem address can be different\):

```text
[ Press Ctrl+C to exit ]
/dev/tty.usbmodem not found.
Select serial port [ /dev/tty.usbmodem1451 ]:
```

Copy the serial port address: `/dev/tty.usbmodem1451` and paste it back:

```text
Select serial port [ /dev/tty.usbmodem1451 ]: /dev/tty.usbmodem1451
```

After you press Enter, you should see an output similar to this:

```text
Resetting device /dev/tty.usbmodem1451...
Connecting: GOPEN:/dev/tty.usbmodem1451,raw,echo=0,clocal=1,cs8,nonblock=1,ixoff=0,ixon=0,ispeed=9600,ospeed=9600,crtscts=0 <-> openssl-connect:blynk-cloud.com:9443,cafile=/Users/.../server.crt,nodelay
2015/10/03 00:29:45 socat[30438.2046857984] N opening character device "/dev/tty.usbmodem1451" for reading and writing
2015/10/03 00:29:45 socat[30438.2046857984] N opening connection to LEN=16 AF=2 45.55.195.102:9443
2015/10/03 00:29:45 socat[30438.2046857984] N successfully connected from local address LEN=16 AF=2 192.168.0.2:56821
2015/10/03 00:29:45 socat[30438.2046857984] N SSL connection using AES128-SHA
2015/10/03 00:29:45 socat[30438.2046857984] N starting data transfer loop with FDs [3,3] and [4,4]
```

**NOTE:** Arduino IDE may complain with "programmer is not responding". You need to terminate script before uploading new sketch.

Additional materials:

* [Tutorial: Control Arduino over USB with Blynk app. No shield required. Mac OS\)](https://www.youtube.com/watch?v=fgzvoan_3_w)
* [How to control arduino \(Wirelessly\) with blynk via USB. Windows](https://www.youtube.com/watch?v=I_hgIj2FdPI)
* [Instructables: Control Arduino with Blynk over USB](http://www.instructables.com/id/Control-arduino-using-Blynk-over-usb/)

## Raspberry Pi

1. Connect your Raspberry Pi to the Internet and open it's console.
2. Run this command \(it updates your OS package repository to include the required packages\):

   ```text
    curl -sL "https://deb.nodesource.com/setup_6.x" | sudo -E bash -
   ```

3. Download and build Blynk JS library using npm:

   ```text
    sudo apt-get update && sudo apt-get upgrade
    sudo apt-get install build-essential
    sudo apt-get install -g npm 
    sudo npm install -g onoff
    sudo npm install -g blynk-library
   ```

4. Run Blynk test script \(put your auth token\):

   ```text
    blynk-client 715f8cafe95f4a91bae319d0376caa8c
   ```

5. You can write our own script based on [examples](https://github.com/vshymanskyy/blynk-library-js/tree/master/examples)
6. To enable Blynk auto restart for Pi, find `/etc/rc.local` file and add there:

   ```text
    node full_path_to_your_script.js <Auth Token>
   ```

Additional materials:

* [Instructables: Blynk on Javascript for Raspberry Pi, Intel Edison and others](http://www.instructables.com/id/Blynk-JavaScript-in-20-minutes-Raspberry-Pi-Edison)
* [Instructables: Use DHT11/DHT12 sensors with Raspberry Pi and Blynk](http://www.instructables.com/id/Raspberry-Pi-Nodejs-Blynk-App-DHT11DHT22AM2302/?ALLSTEPS)

**Note:** Instead of using Node.js, you can also build a C++ libarry version \(same as Arduino, WiringPi-based\) installation:

* [Library README for Linux](https://github.com/blynkkk/blynk-library/blob/master/linux/README.md)
* [Blynk Community Topic: How-To Raspberry Pi](https://community.blynk.cc/t/howto-for-raspberry-pi/332)
* [Video tutorial - Setting up Blynk and Raspberry Pi:](https://www.youtube.com/watch?v=iSG_8g6KyGE)

## ESP8266 Standalone

You can run Blynk directly on the ESP8266!

Install the latest ESP8266 library for Arduino using [this guide](https://github.com/esp8266/Arduino#installing-with-boards-manager).

**Example Sketch:** [ESP8266\_Standalone](https://github.com/blynkkk/blynk-library/blob/master/examples/Boards_WiFi/ESP8266_Standalone/ESP8266_Standalone.ino)

Additional materials:

* [Instructables: ESP8266 ESP-12\(Standalone\)+ Blynk](http://www.instructables.com/id/ESP8266-ESP-12Standalone-Blynk-101)
* [Instructables: ESP8266-12 standalone Blynk lm35 temperature sensor](http://www.instructables.com/id/ESP8266-12-blynk-wireless-temperature-LM35-sensor/?ALLSTEPS)

[Step-by-Step Tutorial in Russian language](http://esp8266.ru/esp8266-blynk)

## NodeMCU

Please follow [this detailed instruction](https://github.com/blynkkk/blynk-library/tree/master/examples/Boards_WiFi/NodeMCU#instruction-for-nodemcu-setup). Or watch [this Video tutorial](https://www.youtube.com/watch?v=FhS44hGk1Lc).

## Arduino + ESP8266 WiFi with AT commands

This connection type is not recommended for beginners.  
If you would like to try it, please carefully read [this help topic](http://help.blynk.cc/hardware-and-libraries/arduino/esp8266-with-at-firmware) **Note:** Some boards like Arduino UNO WiFi from Arduino.org, do not use AT commands \(and do not provide relevant libraries\), so this renders them unusable with Blynk.

## Particle

Blynk works with the whole family of Particle products: Core, Photon and Electron

1. Open [Particle Web IDE](https://build.particle.io/build).
2. Go to the libraries.
3. Search for **Blynk** in the Community Libraries and click on it
4. Open `01_PARTICLE.INO` example
5. Click "use this example"
6. Put your Auth Token here: `char auth[] = "YourAuthToken";` and flash the Particle!

You can scan this QR code from the Blynk App and you'll get a ready-to-test project for **Particle Photon**. Just put your Auth Token into the `01_PARTICLE.INO` example. ![](.gitbook/assets/Particle%20Demo1530733075.png)

Additional materials:

* [Particle core + DHT22](https://www.hackster.io/gusgonnet/temperature-humidity-monitor-with-blynk-7faa51)

