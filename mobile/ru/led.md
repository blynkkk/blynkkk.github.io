
### Светодиод (LED)

A simple LED for indication. You need to send 0 in order to turn LED off. And 255 in order to turn LED on. Or just use
Blynk API as described below :

Простой светодиод для индикации. Вам нужно отправить 0, чтобы выключить светодиод. И 255 для того, чтобы включить светодиод.
Или просто используйте Blynk API, как описано ниже:

```cpp
//регистрируемся на виртуальном пине 1
WidgetLED led1(V1);
led1.off();
led1.on();
```
    
Все значения от 0 до 255 изменяют яркость светодиода:

```cpp
WidgetLED led2(V2);
//установить яркость светодиода на 50%.
led2.setValue(127); 
```

 Вы также можете изменить цвет светодиода с помощью кода:

```cpp
//#D3435C - Красный в RGB формате
Blynk.setProperty(V1, "color", "#D3435C"); 
```

#### Светодиод на главном экране

You can also add LED to your Android Home Screen. LED works via HTTPS in that case. Have in mind that in "Home Screen" 
mode LED has few limitations. LED will update it's state only once per 15 min. You can change this via Widget 
Settings. However update interval less than 15 minutes is not guaranteed.

Вы можете добавить виджет светодиод на домашний экран Android. В этом случае светодиод работает через протокол HTTPS. Имейте в виду, что в режиме «Главный экран» светодиод имеет некоторые ограничения. Светодиод будет обновлять свое состояние только один раз в 15 минут. Вы можете изменить этот интервал через настройки виджета. Однако интервал обновления менее 15 минут не гарантируется.

**Примечание:** Добавление виджета на домашний экран стоит 100 энергии. Эта энергия не возвращается.
**Примечание:** Виджеты главного экрана для локальных серверов Blynk требуют открытия порта 8080.

**Пример кода:** [Светодиод](https://github.com/blynkkk/blynk-library/blob/master/examples/Widgets/LED/LED_Blink/LED_Blink.ino)
