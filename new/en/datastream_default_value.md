### Data stream default value

Default value is a data stream property that allows you to set the initial value for your hardware.
It is most useful on the first device connection to the server.

Let's consider the next use case - You have a light bulb and right after the first device connection  
to the server you want it to be turned on. For that you set the default value for the Virtual Data Stream 
on pin ```V1``` to ```1```. You'll need the next code on the hardware:


```cpp
BLYNK_CONNECTED() {
  Blynk.sync(V1);
}

BLYNK_WRITE(V1)
{
    int bulbValue = param.asInt(); // here you get default value 1
    handle(bulbValue);
}
```

The beauty of this method is you can change the default value of the product at any time,
even hardware was alrady shipped to your clients, without need in OTA.