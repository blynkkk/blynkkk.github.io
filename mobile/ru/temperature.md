
### Температура (Temperature)

Temperature is kind of [environment sensors](https://developer.android.com/guide/topics/sensors/sensors_environment.html) 
that allows you to measure ambient air temperature.
Measured in ```°C``` - celcius.

Температура является своего рода [датчиком окружающей среды](https://developer.android.com/guide/topics/sensors/sensors_environment.html) который позволяет измерять температуру окружающего воздуха. Измеряется в ```°C``` - градусах Цельсия.

Для приема данных из виджета, необходимо использовать код:

```cpp
BLYNK_WRITE(V1) {
  // температура в градусах цельсия
  int celcius = param.asInt();
}
```

Виджет Температуры не работает в фоновом режиме.
