
### Свет (Light)

Light is kind of [environment sensors](https://developer.android.com/guide/topics/sensors/sensors_environment.html) 
that allows you to measure level of light (measures the ambient light level (illumination) in lx).
In phones it is used to control screen brightness.

In order to accept data from it you need to : 

Свет - это своего рода [датчики окружающей среды](https://developer.android.com/guide/topics/sensors/sensors_environment.html), который позволяет измерять уровень освещенности (уровень внешней освещенности измеряется в люксах). В телефонах чаще всего используется для управления яркостью экрана.

Для того, чтобы принять данные этого виджета, вам необходимо:

```cpp
BLYNK_WRITE(V1) {
  //уровень освещенности
  int lx = param.asInt(); 
}
```

Виджет Свет не работает в фоновом режиме.
