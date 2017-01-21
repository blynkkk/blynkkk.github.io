
### Акселерометр

Акселерометр один из [сенсоров движения](https://developer.android.com/guide/topics/sensors/sensors_motion.html), 
который позволяет определить движение Вашего телефона в пространстве. Он может пригодится для отслеживания таких  
событий как тряска, удар, поворот или наклон телефона. Концептуально, акселерометр определяет силу ускорения приложенную 
к вашему телефону. Единица измерения - м/c^2 приложенная к каждой из осей ```x```, ```y```, ```z```.

Чтобы получить данные с сенсора нужно использовать следующий код :

```cpp
BLYNK_WRITE(V1) {
  //acceleration force applied to axis x
  int x = param[0].asFloat(); 
  //acceleration force applied to axis y
  int y = param[1].asFloat();
  //acceleration force applied to axis y
  int z = param[2].asFloat();
}
```

Акселерометр не работает при свернутом приложении.
