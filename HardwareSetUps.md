#Hardware set-ups
## Arduino over USB (no shield)
If you don't have any shield and your hardware doesn't have any connectivity, you can still use Blynk – directly over USB :

1. Open [Arduino Serial USB example](https://github.com/blynkkk/blynk-library/blob/master/examples/BoardsAndShields/Arduino_Serial_USB/Arduino_Serial_USB.ino) 
and change [Auth Token](http://docs.blynk.cc/#getting-started-getting-started-with-application-4-auth-token)

	```cpp
	#include <SoftwareSerial.h>
	SoftwareSerial SwSerial(2, 3); // RX, TX
	#define BLYNK_PRINT SwSerial
	#include <BlynkSimpleSerial.h>
	
	// You should get Auth Token in the Blynk App.
	// Go to the Project Settings (nut icon).
	char auth[] = "YourAuthToken";
	
	void setup()
	{
	  SwSerial.begin(9600);
	  Blynk.begin(auth);
	  // Default baud rate is 9600. You could specify it like this:
	  //Blynk.begin(auth, 57600);
	}
	
	void loop()
	{
	  Blynk.run();
	}
	```
2. Run the script which is usually located in ```/scripts``` folder:

 - Windows:```My Documents\Arduino\libraries\Blynk\scripts```
 - Mac	```User$/Documents/Arduino/libraries/Blynk/scripts```

  
  **On Windows:**
  
  Open cmd.exe
  
  Write your path to blynk-ser.bat folder. For example:
   
```
cd C:\blynk-library-0.3.1\blynk-library-0.3.1\scripts
```
  
  Run ```blynk-ser.bat``` file. For example : ```blynk-ser.bat -c COM4``` (where COM4 is port with your Arduino)
  
  And press "Enter", press "Enter" and press "Enter"
  
  **On Linux and Mac**:
  
  Navigate to /scripts folder. For example:
  
```
cd User$/Documents/Arduino/libraries/Blynk/scripts
``` 

  When inside this folder, run:
  
```
user:scripts User$ ./blynk-ser.sh
``` 
  
  You may need to run it with ```sudo```
  
```
user:scripts User$ sudo ./blynk-ser.sh
``` 

  This is what you'll see in Terminal app on Mac (usbmodem address can be different):
  
```
[ Press Ctrl+C to exit ]
/dev/tty.usbmodem not found.
Select serial port [ /dev/tty.usbmodem1451 ]: 
```
	
  Copy the serial port address: ```/dev/tty.usbmodem1451``` and paste it back:

```
Select serial port [ /dev/tty.usbmodem1451 ]: /dev/tty.usbmodem1451
```
	
  After you press Enter, you should see an output similar to this:

```
Resetting device /dev/tty.usbmodem1451...
Connecting: GOPEN:/dev/tty.usbmodem1451,raw,echo=0,clocal=1,cs8,nonblock=1,ixoff=0,ixon=0,ispeed=9600,ospeed=9600,crtscts=0 <-> openssl-connect:cloud.blynk.cc:8441,cafile=/Users/.../server.crt,nodelay
2015/10/03 00:29:45 socat[30438.2046857984] N opening character device "/dev/tty.usbmodem1451" for reading and writing
2015/10/03 00:29:45 socat[30438.2046857984] N opening connection to LEN=16 AF=2 45.55.195.102:8441
2015/10/03 00:29:45 socat[30438.2046857984] N successfully connected from local address LEN=16 AF=2 192.168.0.2:56821
2015/10/03 00:29:45 socat[30438.2046857984] N SSL connection using AES128-SHA
2015/10/03 00:29:45 socat[30438.2046857984] N starting data transfer loop with FDs [3,3] and [4,4]
```

<span style="color:#D3435C;">**NOTE:** Arduino IDE may complain with "programmer is not responding". You need to terminate script before uploading new sketch. </span>

Additional materials:

- [Instructables: Control Arduino with Blynk over USB](http://www.instructables.com/id/Control-arduino-using-Blynk-over-usb/)


## Raspberry Pi
1. Connect your Raspberry Pi to the Internet and open it's console.
2. Follow the [tutorial to install Node.js](https://learn.adafruit.com/node-embedded-development/installing-node-dot-js)
3. Download and build Blynk JS library using npm:


	```bash
	sudo apt-get update && sudo apt-get upgrade
	sudo apt-get install build-essential
	sudo npm install -g npm
	sudo npm install -g onoff
	sudo npm install -g blynk-library
	```

4. Run Blynk test script (put your auth token):

	```bash
	blynk.js 715f8cafe95f4a91bae319d0376caa8c
	```
5. You can write our own script based on [examples](https://github.com/vshymanskyy/blynk-library-js/tree/master/examples)

6. To enable Blynk auto restart for Pi, find ```/etc/rc.local``` file and add there:

	```
	node full_path_to_your_script.js <Auth Token> 
	```

Additional materials:

- [Instructables: Blynk on Javascript for Raspberry Pi, Intel Edison and others](http://www.instructables.com/id/Blynk-JavaScript-in-20-minutes-Raspberry-Pi-Edison)
- [Instructables: Use DHT11/DHT12 sensors with Raspberry Pi and Blynk](http://www.instructables.com/id/Raspberry-Pi-Nodejs-Blynk-App-DHT11DHT22AM2302/?ALLSTEPS)

For C++ (WiringPi-based) installation:

- [Blynk Community Topic: How-To Raspberry Pi](http://community.blynk.cc/t/howto-for-raspberry-pi/332)
- [Video tutorial - Setting up Blynk and Raspberry Pi:](https://www.youtube.com/watch?v=iSG_8g6KyGE)
<iframe width="200" height="110" src="https://www.youtube.com/embed/iSG_8g6KyGE" frameborder="0" allowfullscreen></iframe>

## ESP8266 Standalone

You can run Blynk directly on the ESP8266!

Install the latest ESP8266 library for Arduino using [this guide](https://github.com/esp8266/Arduino#installing-with-boards-manager). 

**Example Sketch:** [ESP8266_Standalone](https://github.com/blynkkk/blynk-library/blob/master/examples/BoardsAndShields/ESP8266_Standalone/ESP8266_Standalone.ino)

Additional materials:

- [Instructables: ESP8266 ESP-12(Standalone)+ Blynk](http://www.instructables.com/id/ESP8266-ESP-12Standalone-Blynk-101)
- [Instructables: ESP8266-12 standalone Blynk lm35 temperature sensor](http://www.instructables.com/id/ESP8266-12-blynk-wireless-temperature-LM35-sensor/?ALLSTEPS)
 
[Step-by-Step Tutorial in Russian language](http://esp8266.ru/esp8266-blynk)

## Particle (formely Spark)
Blynk works with the whole family of Particle products: Core, Photon and Electron(soon)

TODO:

1. Open [Particle Web IDE](https://build.particle.io/build).
2. Go to the libraries.
3. Search for **Blynk** in the Community Libraries and click on it
4. Open ```01_PARTICLE.INO``` example
5. Click "use this example"
6. Put your Auth Token here: ``` char auth[] = "YourAuthToken";``` and flash the Particle!

On Android, you can scan this QR code from Blynk App and you'll get a ready-to-test project for **Particle Photon**. Just put your Auth Token to the ```01_PARTICLE.INO``` example.
<img src="images/Particle Demo1530733075.png" style="width: 300px; height:300px"/>

Additional materials:

- [Particle core + DHT22](https://www.hackster.io/gusgonnet/temperature-humidity-monitor-with-blynk-7faa51)
