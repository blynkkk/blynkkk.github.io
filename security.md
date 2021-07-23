# Security

Blynk server has 5 ports open for different security levels.

* **80** - plain TCP connection for the hardware \(no security\)
* **8080** - plain TCP connection for hardware \(no security\)
* **443** - SSL/TLS connection for the Mobile Apps and hardware with SSL
* **9443** - SSL/TLS connection for the Mobile Apps and hardware with SSL

Hardware may select to connect to 443 \(9443\) or 80 \(8080\), depending on it's capabilities. Connection between the app and the server is always is done through SSL/TLS, so it is always secured. Connection between the hardware and server depends on your hardware capabilities.

## Use Local Blynk Server

Local Blynk Server is no longer supported.

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

