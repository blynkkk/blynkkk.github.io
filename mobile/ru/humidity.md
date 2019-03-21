### Влажность (Humidity)

Humidity is kind of [environment sensors](https://developer.android.com/guide/topics/sensors/sensors_environment.html) 
that allows you to measure ambient relative humidity.

Measured in ```%``` - actual relative humidity in percent.

In oder to accept data from it you need to : 

Влажность является своего рода [датчиком среды](https://developer.android.com/guide/topics/sensors/sensors_environment.html),
который позволяет измерять относительную влажность окружающей среды.

Измеряется в ```%``` - фактически относительная влажность в процентах.

Для того, чтобы принять данные от датчика, вам необходимо:

```cpp
BLYNK_WRITE(V1) {
  //Влажность в %
  int humidity = param.asInt();
}
```

**ВНИМАНИЕ:** Влажность не работает в фоновом режиме.
