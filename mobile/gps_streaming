
### GPS Streaming

Useful for monitoring device location data: such as latitude, longitude, altitude, and speed (but it could be often 0, 
if device could not provide it).

In order to accept data from it you need to : 

```cpp
BLYNK_WRITE(V1) {
  float latitude = param[0].asFloat(); 
  float longitude = param[1].asFloat();
  float altitude = param[2].asFloat();
  float speed = param[2].asFloat();
}
```

GPS Streaming works in background.
