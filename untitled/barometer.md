# Barometer/pressure

Barometer/pressure is kind of [environment sensors](https://developer.android.com/guide/topics/sensors/sensors_environment.html) that allows you to measure the ambient air pressure.

Measured in in `hPa` or `mbar`.

In oder to accept data from it you need to :

```cpp
BLYNK_WRITE(V1) {
  //pressure in mbar
  int pressure = param[0].asInt(); 
}
```

Barometer doesn't work in background.

