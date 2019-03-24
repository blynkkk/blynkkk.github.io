
### Значение переменной (Labeled Value)

Отображает входящие данные с ваших датчиков или виртуальных пин-ов. Это лучшая версия «Отображения значений», так как в ней есть строка форматирования, так что вы можете форматировать входящее значение в любую нужную вам строку.

 Может работать в 2 режимах:

- режим PUSH (выбирается из списка частоты считывания);
- режим частоты считывания.

 В режиме PUSH вы обновляете значения виджета со стороны аппаратного устройства с помощью кода:
 
```cpp
Blynk.virtualWrite(V1, val); 
```

В этом режиме каждое сообщение, которое аппаратное обеспечение отправляет на сервер, автоматически сохраняется на сервере. Режим PUSH не требует, чтобы приложение было онлайн или запущено.

В режиме частоты считывания вам нужно выбрать интервал обновления, и приложение будет запускать события с требуемым интервалом. Ваше приложение должно быть открыто и запущено для отправки запросов на оборудование.  В этом случа вам не нужен код для аналоговых и цифровых пин-ов. Однако для виртуальных пин-ов вам необходимо использовать следующий код:

```cpp
//взызов из приложения
BLYNK_READ(V1)
{
  //отправка в приложение
  Blynk.virtualWrite(V1, val);
}
```

#### Formatting options

Let's assume, your sensor sends number 12.6789 to Blynk application.
Next formatting options are supported:

```/pin/``` - displays the value without formatting (12.6789)

```/pin./``` - displays the value without decimal part (13)

```/pin.#/``` - displays the value with 1 decimal digit (12.7)

```/pin.##/``` - displays the value with two decimal places (12.68)

#### Home Screen Labeled Value

You can also add Labeled Value to your Android Home Screen. Labeled Value works via HTTPS in that case. 
Have in mind that in "Home Screen" mode Labeled Value has few limitations. Labeled Value will update it's state only 
once per 15 min. You can change this via Widget Settings. However update interval less than 15 minutes is not guaranteed. 
You can also resize Labeled Value on Home Screen - just do long click on widget and resize it as you need.

**Note :** Adding home screen widget costs 100 energy. This energy not rechargeable.
**Note :** Home Screen Widgets for Local Blynk servers requires port 8080 to be opened.

**Sketch:** [BlynkBlink](https://github.com/blynkkk/blynk-library/blob/master/examples/GettingStarted/BlynkBlink/BlynkBlink.ino)
