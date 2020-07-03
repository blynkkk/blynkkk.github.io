# Events: Code

Event code is used in firmware API to trigger and render events from the device.

**IMPORTANT:** Event code should be unique within the product.

## How to trigger events:

If you need to create a warning when the sensor detects temperature over a certain threshold. 1. Create a new Warning event named `High temperature` with code `high_temp` 2. Use the `Blynk.logEvent(event_code)` to trigger new event occurrence 3. When the device triggers the event, it will be rendered on the Timeline

A simple example could look like:

```cpp
if (temperatureSensor > 35)
{
   Blynk.logEvent("high_temp");
}
```

You can also use HTTPS API in order to trigger the device event:

```text
/external/api/logEvent?token={device_token}&code={event_code}&description={event_desciption}
```

`description` is an optional parameter where you can attach additional information to be rendered on the Timeline along with the event.

For example:

```text
https://my.server.com/external/api/logEvent?token=Q9qdlGahPuFuCfncrT35QutT7s3HjYFy&code=high_temp
```

