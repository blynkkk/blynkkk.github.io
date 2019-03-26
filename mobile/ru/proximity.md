
### Proximity

Proximity is kind of [position sensors](https://developer.android.com/guide/topics/sensors/sensors_position.html) 
that allows you to determine how close the face of a smartphone is to an object.
Measured in ```cm``` - distance from phone face to object. However most of this sensors returns only FAR / NEAR information.
So return value will be ```0/1```. Where 0/LOW  is ```FAR``` and 1/HIGH is ```NEAR```.

In order to accept data from it you need to : 

```cpp
BLYNK_WRITE(V1) {
  // distance to object
  int proximity = param.asInt();
  if (proximity) {
     //NEAR
  } else {
     //FAR
  }
}
```

Proximity doesn't work in background.
