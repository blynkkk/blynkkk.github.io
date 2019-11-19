### Datastream: Sync with latest server value

This setting enables the device to sync with the latest known value on the server.

For example, user owns a wi-fi connected dimmer light
1. Device goes offline
2. User sets brightness of the light to 100
3. When device comes online, it will request the latest value from the server and set brightness to 100

To sync device to the latest state, use the firmware API commands: ```Blynk.sync()``` or ```Blynk.syncAll()```.

Example: 
```cpp
BLYNK_CONNECTED() { // when device is conneceted to Blynk Cloud...
  Blynk.syncAll(); // request the values for all datastreams that has "sync" setting enabled
}
```

**IMPORTANT:** When this setting is disabled, neither ```Blynk.sync()``` nor ```Blynk.syncAll()```
