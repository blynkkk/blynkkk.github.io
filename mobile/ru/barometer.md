
### Барометр/Давление

Барометр один из сенсоров [окружающей среды](https://developer.android.com/guide/topics/sensors/sensors_environment.html) 
и позволяет измерять атмосферное давление.

Измеряется в ```hPa``` или ```mbar```.

Чтобы получить данные с сенсора нужно использовать следующий код :

```cpp
BLYNK_WRITE(V1) {
  //pressure in mbar
  int pressure = param[0].asInt(); 
}
```

Акселерометр не работает при свернутом приложении.
