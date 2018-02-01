#Security

Blynk server has 3 ports open for different security levels.

* **8441** - SSL/TLS connection for hardware
* **8442** - plain TCP connection for hardware (no security)
* **443** - mutual authentication (mutual SSL) connection for Mobile Apps

Hardware may select to connect to 8441 or 8442, depending on it's capabilities.

#### Use SSL gateway

Most platforms are not capable to handle SSL, so they connect to 8442.
However, our [gateway script](https://github.com/blynkkk/blynk-library/blob/master/scripts/blynk-ser.sh) can be used to add SSL security layer to communication.

```bash
./blynk-ser.sh -f SSL
```
This will forward all hardware connections from 8441 port to the server via SSL gateway.
You can run this script on your Raspberry Pi, desktop computer, or even directly on your router!

**Note:** when using your own server, you should overwrite the bundled server.crt certificate, or specify it to the script using ```--cert``` switch:

```bash
./blynk-ser.sh -f SSL -s <server ip> -p 8441 --cert=<certificate>.crt
```

Flag ```-f SSL``` is enabled by default for USB communication so you don't have to explicit declare it.

**Note:** SSL is supported by the gateway only on Linux/OSX for now
 
If you want to skip SSL, and connect to TCP, you can also do that:

```bash
./blynk-ser.sh -t TCP
```

#### Use Local Blynk Server

In order to gain maximum security you could [install Blynk server locally](http://docs.blynk.cc/#blynk-server) and 
restrict access to your network, so nobody except you could access it. In this case all data is stored locally within
your network and not send via Internet.

In case of Local Blynk Server there is also no need to protect connection between your hardware and Local Blynk Server.
This is true for Ethernet connection and partially true for Wi-Fi connection. In case of Wi-Fi you have to use at least 
WPA, WPA2 (Wi-Fi Protected Access) Wi-Fi type in order to protect wireless traffic. 

WPA and WPA2 offer a very robust encryption that is likely to protect all data travelling over the air—given that 
a strong enough password is used. Even if your data is plain TCP/IP, another user won't be able to decipher captured 
packets. Still, make sure that your password is strong enough, otherwise the only limiting factor for an attacker is time.
