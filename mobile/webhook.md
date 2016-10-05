
### Webhook

Webhook is a widget for 3-d party integrations. With webhook widget you can send HTTP/S requests to any 3-d party server 
or device that has HTTP/S API (Philips Hue for instance).

Any write operation from hardware side will trigger webhook widget (same way as for eventor). You can also trigger 
webhook from application side in case control widget assigned to same pin as webhook. You can trigger 3-d party service 
with single button click.

For example, imagine a case when you want to send data from your hardware not only to Blynk but also to Thingspeak server.
In typical, classic use case you'll need to write code like this (this is minimal and not full sketch) : 

```
WiFiClient client;
if (client.connect("api.thingspeak.com", 80)) {
    client.print("POST /update HTTP/1.1\n");
    client.print("Host: api.thingspeak.com\n");
    client.print("Connection: close\n");
    client.print("X-THINGSPEAKAPIKEY: " + apiKeyThingspeak1 + "\n");
    client.print("Content-Type: application/x-www-form-urlencoded\n");
    client.print("Content-Length: ");
    client.print(postStr.length());
    client.print("\n\n");
    client.print(postStr);
}
```
 
With webhook widget this is not necessary anymore. All you need just fill below fields : 

<img src="images/webhook_settings.png" style="width: 200px; height:360px"/>

And do usual :  

```
Blynk.virtualWrite(V0, value);
```

where V0 is pin assigned to webhook widget.

Also you can use usual Blynk placeholders for pin value in body or url, for example : 

```
https://api.thingspeak.com/update?api_key=xxxxxx&field1=/pin/
```

or for body

```
["/pin/"]
```

You can also refer to specific index of multi value pin : 

```/pin0/```,```/pin1/```, ```/pin2/```

Another cool thing about webhook is that you can make GET requests from Blynk Server side and return response directly to
your hardware. The beauty here is that you don't need to code request to 3-d party service. Imagine a case when you want to get 
weather from some 3-d party service. For example, you have an url 
```http://api.sunrise-sunset.org/json?lat=33.3823&lng=35.1856&date=2016-10-01```, you can put it in widget, select ```V0``` pin,
and do usual :  

```
BLYNK_WRITE(V0){
  String webhookdata = param.asStr();
  Serial.println(webhookdata);
}
```

Now, every time you'll trigger ```V0``` pin (with ```Blynk.virtualWrite(V0, 1)``` from hardware side or with control widget
assigned to ```V0```) - ```BLYNK_WRITE(V0)``` will be triggered.

**NOTE :** usually 3-d party servers returns big responses, so you have to increase hardware maximum allowed message size with 
```#define BLYNK_MAX_READBYTES 1024```. Where ```1024``` - is maximum allowed message size.

**NOTE :** Blynk cloud has limitation for webhook widget - you are allowed to send only 1 request per second. You can
 change this on local server with ```webhooks.frequency.user.quota.limit```. Please be very careful using webhooks, 
 as many resources not capable to handle even 1 req/sec, so you may be banned on some of them. For example thingspeak 
 allows to send 1 request per 15 seconds.