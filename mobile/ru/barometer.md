
### Барометр/Давление (Barometer/pressure)

Барометр один из сенсоров [окружающей среды](https://developer.android.com/guide/topics/sensors/sensors_environment.html) 
и позволяет измерять атмосферное давление.

Измеряется в ```hPa``` (гПа) или ```mbar``` (мБар).

Чтобы получить данные с сенсора нужно использовать следующий код :

```cpp
BLYNK_WRITE(V1) {
  //Давление в мБар
  int pressure = param[0].asInt(); 
}
```

Барометр не работает при свернутом приложении.
