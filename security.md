# Security

Blynk server has 5 ports open for different security levels.

* **80** - plain TCP connection for the hardware \(no security\)
* **8080** - plain TCP connection for hardware on the Local Server \(no security\)
* **443** - SSL/TLS connection for the Mobile Apps and hardware with SSL
* **9443** - SSL/TLS connection for the Mobile Apps on the Local Server and hardware with SSL

Hardware may select to connect to 443 \(9443\) or 80 \(8080\), depending on it's capabilities. Connection between the app and the server is always is done through SSL/TLS, so it is always secured. Connection between the hardware and server depends on your hardware capabilities. With the Local Blynk server connection type between the hardware and server is not that important for the security as the Local server is usually placed within the local network, so attacker can't intercept traffic between hardware and the server.

## Use Local Blynk Server

In order to gain maximum security you could [install Blynk server locally](./#blynk-server) and restrict access to your network, so nobody except you could access it. In this case all data is stored locally within your network and not send via Internet.

In case of Local Blynk Server there is also no need to protect connection between your hardware and Local Blynk Server. This is true for Ethernet connection and partially true for Wi-Fi connection. In case of Wi-Fi you have to use at least WPA, WPA2 \(Wi-Fi Protected Access\) Wi-Fi type in order to protect wireless traffic.

WPA and WPA2 offer a very robust encryption that is likely to protect all data travelling over the air—given that a strong enough password is used. Even if your data is plain TCP/IP, another user won't be able to decipher captured packets. Still, make sure that your password is strong enough, otherwise the only limiting factor for an attacker is time.

## Use SSL gateway

Most platforms are not capable to handle SSL, so they connect to 80. However, our [gateway script](https://github.com/blynkkk/blynk-library/blob/master/scripts/blynk-ser.sh) can be used to add SSL security layer to communication.

```bash
./blynk-ser.sh -f SSL
```

This will forward all hardware connections from 9443 port to the server via SSL gateway. You can run this script on your Raspberry Pi, desktop computer, or even directly on your router!

**Note:** when using your own server, you should overwrite the bundled server.crt certificate, or specify it to the script using `--cert` switch:

```bash
./blynk-ser.sh -f SSL -s <server ip> -p 9443 --cert=<certificate>.crt
```

Flag `-f SSL` is enabled by default for USB communication so you don't have to explicit declare it.

**Note:** SSL is supported by the gateway only on Linux/OSX for now

If you want to skip SSL, and connect to TCP, you can also do that:

```bash
./blynk-ser.sh -t TCP
```

