### Events: Code

Event code defines a string that you can use in order to trigger the event. 
For example, let's assume you created a warning event ```High temperature``` with code ```high_temp```.
Now you can trigger it (make it appear in the timeline of the device) with the next code from your hardware:

```
Blynk.logEvent("high_temp");
```

You can also use a HTTPS API:

```
/external/api/logEvent?token={device_token}&code={event_code}&description={event_desciption}
```

For example:
```
https://my.server.com/external/api/logEvent?token=Q9qdlGahPuFuCfncrT35QutT7s3HjYFy&code=high_temp
```