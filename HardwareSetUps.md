#Hardware set-ups
## Arduino over USB (no shield)
If you don't have any shield and your hardware doesn't have any connectivity, you can still use Blynk – directly over USB :

1. Upload [sketch below](https://github.com/blynkkk/blynk-library/blob/master/examples/BoardsAndShields/Arduino_Serial_USB/Arduino_Serial_USB.ino) 
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
2. Run the script  which is located in "scripts" folder of library root, e.g. 'blynk-library/scripts`
  
  **On Windows:**
    1. Open cmd.exe
    2. Write your path to blynk-ser.bat folder. For example: 
    ```
    cd C:\blynk-library-0.3.1\blynk-library-0.3.1\scripts
    ```
    3. Run ```blynk-ser.bat``` file. For example : ```blynk-ser.bat -c COM4``` (where COM4 is port with your Arduino)
    4. And press "Enter", press "Enter" and press "Enter"
  
  **On Linux and Mac** use: 
  
  ```
  ./blynk-ser.sh
  ``` 
  You may need to run it with ```sudo```

This is what you'll see in Terminal app on Mac (usbmodem address can be different):

```
[ Press Ctrl+C to exit ]
/dev/tty.usbmodem not found.
Select serial port [ /dev/tty.usbmodem1451 ]: 
```
Select and copy this serial port address(```/dev/tty.usbmodem1451```) and paste it back:

```
Select serial port [ /dev/tty.usbmodem1451 ]: /dev/tty.usbmodem1451
```

After you press Enter, you should see something similar:

```
Resetting device /dev/tty.usbmodem1451...
Connecting: GOPEN:/dev/tty.usbmodem1451,raw,echo=0,clocal=1,cs8,nonblock=1,ixoff=0,ixon=0,ispeed=9600,ospeed=9600,crtscts=0 <-> openssl-connect:cloud.blynk.cc:8441,cafile=/Users/.../server.crt,nodelay
2015/10/03 00:29:45 socat[30438.2046857984] N opening character device "/dev/tty.usbmodem1451" for reading and writing
2015/10/03 00:29:45 socat[30438.2046857984] N opening connection to LEN=16 AF=2 45.55.195.102:8441
2015/10/03 00:29:45 socat[30438.2046857984] N successfully connected from local address LEN=16 AF=2 192.168.0.2:56821
2015/10/03 00:29:45 socat[30438.2046857984] N SSL connection using AES128-SHA
2015/10/03 00:29:45 socat[30438.2046857984] N starting data transfer loop with FDs [3,3] and [4,4]
```

<span style="color:#D3435C;">**NOTE:** Arduino IDE may complain with "programmer is not responding". You need to terminate script before uploading new sketch.. </span>

Here are some additional materials :

- [Instructables](http://www.instructables.com/id/Control-arduino-using-Blynk-over-usb/)


## Raspberry Pi
1. Connect your Raspberry Pi to the internet and open it's console.
2. Install WiringPi: http://wiringpi.com/download-and-install/
3. Download and build Blynk:
```bash
$ git clone https://github.com/blynkkk/blynk-library.git
$ cd blynk-library/linux
$ make clean all target=raspberry
```
4. Run Blynk:
```bash
$ sudo ./blynk --token=YourAuthToken
```
5. To enable Blynk auto restart for Pi find */etc/init.d/rc.local* file and add
```
/FULL_PATH_TO_LIB/blynk-library/linux/blynk --token=<Auth Token> 
```
For example:
``` 
/home/pi/blynk-library/linux/blynk --token=<my token> &
```

We have also provided a build script, you can try just running (inside of the "linux" directory):
```bash
$ ./build.sh raspberry
```

Additional materials:

- [Instructables](http://www.instructables.com/id/Blynk-JavaScript-in-20-minutes-Raspberry-Pi-Edison)
- [Forum discussion](http://community.blynk.cc/t/howto-for-raspberry-pi/332)
- [Video tutorial](https://www.youtube.com/watch?v=iSG_8g6KyGE)

## ESP8266 (standalone)

You can run Blynk directly on the ESP8266!

Install the latest ESP8266 for Arduino using [this guide](https://github.com/esp8266/Arduino#installing-with-boards-manager). Also [here](http://www.instructables.com/id/ESP8266-ESP-12Standalone-Blynk-101) and [here russian](http://esp8266.ru/esp8266-blynk) is step-by-step tutorial.

**Sketch:** [ESP8266_Standalone](https://github.com/blynkkk/blynk-library/blob/master/examples/BoardsAndShields/ESP8266_Standalone/ESP8266_Standalone.ino)

## Particle (formely Spark)
Blynk works with the whole family of Particle products: Core, Photon and Electron (soon)

TODO:
>Add screenshots for steps

1. Open [Particle Web IDE](https://build.particle.io/build).
2. Go to the libraries.
3. Search for **Blynk** in the Community Libraries and click on it.
4. Open SparkCore.ino example.
5. Click "use this example".
6. Update your auth token, and upload!
