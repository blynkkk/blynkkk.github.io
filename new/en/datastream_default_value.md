### Datastream: Default Value

Default Value is a setting that allows you to set the initial value for the Datastream.
This value later can be used in hardware API, HTTPS API, or within Rule Engine.
Usually, this setting is used to set the initial value when hardware boots up for the first time.

Example: 
You are working on a smart light bulb and would like to turn it on when it first connects to the server after provisioning.

Set the default value for the Datastream ```V1``` to ```1```. 
Then use this code on the hardware:

```cpp
BLYNK_CONNECTED() {
  // request the V1 value on connect
  // for initial connect it will be default value 1
  Blynk.sync(V1);
}

BLYNK_WRITE(V1)
{
    // here you get default value 1
    int bulbValue = param.asInt();
    handle(bulbValue);
}
```

You can change the default value of the product at any time. 
There is no need to update firmware over-the-air even when the product was already shipped to your clients.
