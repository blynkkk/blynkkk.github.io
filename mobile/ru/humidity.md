
### Humidity

Humidity is kind of [environment sensors](https://developer.android.com/guide/topics/sensors/sensors_environment.html) 
that allows you to measure ambient relative humidity.

Measured in ```%``` - actual relative humidity in percent.

In oder to accept data from it you need to : 

```cpp
BLYNK_WRITE(V1) {
  // humidity in %
  int humidity = param.asInt();
}
```

Humidity doesn't work in background.
