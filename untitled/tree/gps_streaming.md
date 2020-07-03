# Поток GPS \(GPS Streaming\)

Полезно для мониторинга местонахождения смартфона получать данные о широте, долготе, высоте и скорости \(скорость часто может быть 0, если смартфон не поддерживает ее измерение\).

Чтобы принимать данные из этого виджета, вам необходимо:

```cpp
BLYNK_WRITE(V1) {
  float latitude = param[0].asFloat(); 
  float longitude = param[1].asFloat();
  float altitude = param[2].asFloat();
  float speed = param[3].asFloat();
}
```

или вы можете использовать подготовленную оболочку `GpsParam` :

```cpp
BLYNK_WRITE(V1) {
  GpsParam gps(param);
  //Печать лат/лон с 6 десятичными знаками
  Serial.println(gps.getLat(), 7);
  Serial.println(gps.getLon(), 7);

  Serial.println(gps.getAltitude(), 2);
  Serial.println(gps.getSpeed(), 2);
}
```

Поток GPS работает в фоновом режиме.

**Пример кода:** [Поток GPS](https://github.com/blynkkk/blynk-library/blob/master/examples/Widgets/GPS_Stream/GPS_Stream.ino)

