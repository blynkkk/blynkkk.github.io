### Datastream: Sync with the latest server value

This setting enables the device to sync with the latest known value on the server.

For example, a user owns a wi-fi connected dimmer light
1. The device goes offline
2. User sets the brightness of the light to 100% in the mobile app 
3. When the device comes back online, it will request the latest value from the server and set brightness to 100


To sync the device to the latest state, use the firmware API commands: ```Blynk.sync()``` or ```Blynk.syncAll()```.

```cpp
BLYNK_CONNECTED() { // when device is conneceted to Blynk Cloud...
  Blynk.syncAll(); // request the values for all datastreams that has "sync" setting enabled
}
```

**IMPORTANT:** When this setting is disabled for a Datastream, neither ```Blynk.sync()``` nor ```Blynk.syncAll()``` will work.
