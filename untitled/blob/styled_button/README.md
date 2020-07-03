# Стилизованная кнопка \(Styled Button\)

Работает в режиме кнопки или выключателя. Позволяет отправить любое числовое значение при нажатии и отпускании кнопки. По умолчанию кнопка использует значения 0/1 \(HIGH/LOW\). Кнопка при нажатии отправляет 1 \(HIGH\) а при отпускании отправляет 0 \(LOW\).

Вы можете изменить состояние кнопки со стороны оборудования. Например, включить кнопку, назначенную виртуальному пин-у V1:

```cpp
Blynk.virtualWrite(V1, HIGH);
```

Вы можете изменить надписи кнопок со стороны оборудования при помощи кода:

```cpp
Blynk.setProperty(V1, "onLabel", "ВКЛ");
Blynk.setProperty(V1, "offLabel", "ВЫКЛ");
```

или изменить цвет кнопки во включенном и выключенном состоянии:

```cpp
Blynk.setProperty(V1, "onColor", "#D3435C");
Blynk.setProperty(V1, "offColor", "#D3435C");
```

или изменить цвет фона кнопки:

```cpp
Blynk.setProperty(V1, "onBackColor", "#00435C");
Blynk.setProperty(V1, "offBackColor", "#00435C");
```

Вы также можете узнать состояние кнопки с сервера, если ваше оборудование внезапно отключилось, с помощью функции Blynk.Sync:

```cpp
BLYNK_CONNECTED() {
  Blynk.syncVirtual(V1);
}

BLYNK_WRITE(V1) {
  int buttonState = param.asInt();
}
```

**Пример кода:** [Базовый пример](https://github.com/blynkkk/blynk-library/blob/master/examples/GettingStarted/BlynkBlink/BlynkBlink.ino)

**Пример кода:** [Синхронизация состояния с физической кнопкой через прерывания](https://github.com/blynkkk/blynk-library/blob/master/examples/More/Sync/ButtonInterrupt/ButtonInterrupt.ino)

**Пример кода:** [Синхронизация состояния с физической кнопкой через поллинг](https://github.com/blynkkk/blynk-library/blob/master/examples/More/Sync/ButtonPoll/ButtonPoll.ino)

**Пример кода:** [Синхронизация состояния с физической кнопкой](https://github.com/blynkkk/blynk-library/blob/master/examples/More/Sync/SyncPhysicalButton/SyncPhysicalButton.ino)

