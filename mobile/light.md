
### Light

Light is kind of [environment sensors](https://developer.android.com/guide/topics/sensors/sensors_environment.html) 
that allows you to measure level of light (measures the ambient light level (illumination) in lx).
In phones it is used to control screen brightness.

In order to accept data from it you need to : 

```cpp
BLYNK_WRITE(V1) {
  //light value
  int lx = param.asInt(); 
}
```

Light doesn't work in background.
