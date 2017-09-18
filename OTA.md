#OTA

Blynk also supports on the air updates for - ESP8266, NodeMCU and SparkFun Blynk boards. OTA supported only 
for the private servers and for the paid customers for now.

How does it work:

 - You need to use [regular sketch for exported apps](https://github.com/blynkkk/blynk-library/tree/master/examples/Export_Demo/Template_ESP8266);
 - After you launched your hardware you are ready for OTA;
 - You can trigger the firmware update for the specific hardware via it's token or for all hardware.

## Trigger update for the specific hardware

```
curl -v -F file=@Template_ESP8266.ino.nodemcu.bin --insecure -u admin@blynk.cc:admin https://localhost:9443/admin/ota/start?token=123
```

 - ```Template_ESP8266.ino.nodemcu.bin``` - is relative (or full) path to your firmware;
 - ```--insecure``` flag for servers with self-generated certificates. You don't need this flag if you used Let's Encrypt or other trusted certificates;
 - ```admin@blynk.cc:admin``` admin credentials to your server. This is default ones. Format is ```username:password```. You can change it in ```server.properties``` file;
 - ```token``` is token of your hardware you want apply the firmware update to. The firmware update will be initiated only in case device is online;

## Trigger OTA for all devices
 
Update for all devices will be triggered only when they are connected to the cloud. You need to remove the token part for that.

```
curl -v -F file=@Template_ESP8266.ino.nodemcu.bin --insecure -u admin@blynk.cc:admin https://localhost:9443/admin/ota/start
```

In that case, OTA will be triggered right after device connected to the server. In case device is online firmware update 
will be initiated only when device will be connected again.

## Trigger OTA for the specific user

In that case firmware update will be triggered for all devices of specified user. 

```
curl -v -F file=@Template_ESP8266.ino.nodemcu.bin --insecure -u admin@blynk.cc:admin https://localhost:9443/admin/ota/start?user=pupkin@gmail.com
```

## Trigger OTA for specific user and project

In that case firmware update will be triggered for all devices of specified user within specified project. 

```
curl -v -F file=@Template_ESP8266.ino.nodemcu.bin --insecure -u admin@blynk.cc:admin https://localhost:9443/admin/ota/start?user=pupkin@gmail.com&project=123
```

## Stop OTA

```
curl -v --insecure -u admin@blynk.cc:admin https://localhost:9443/admin/ota/stop
```

## How to make firmware

In order to make firmware in Arduino IDE - go to menu: Sketch -> Export compiled Binary.


*NOTE:* ESP8266 right now takes firmware only via HTTP. And not HTTPS.