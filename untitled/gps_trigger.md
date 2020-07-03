# GPS Trigger

GPS trigger widget allows easily trigger events when you arrive to or leave from some destination. This widget will work in background and periodically will check your coordinates. In case your location is within/out required radius \(selected on widget map\) widget will send `HIGH`/`LOW` command to hardware. For example, let's assume you have GPS Trigger widget assigned to pin `V1` and option `Trigger When Enter`. In that case when you'll arrive to destination point widget will trigger `HIGH` event.

```cpp
BLYNK_WRITE(V1) {
  int state = param.asInt();
  if (state) {
      //You enter destination
  } else {
      //You leave destination
  }
}
```

More details on how GPS widget works you can read [here](https://developer.android.com/guide/topics/location/strategies.html).

GPS trigger widget works in background.

