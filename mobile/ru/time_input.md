
## Ввод времени (Time Input)

Виджет Ввода времени позволяет вам выбрать время начала/окончания, день недели, часовой пояс, значения в формате до полудня/после полудня и отправить их на ваше оборудование. В настоящее время поддерживаются следующие форматы: ```ЧЧ:ММ``` и ```ЧЧ:ММ AM/PM```.

Аппаратное устройстов будет отсчитывать время пользовательского интерфейса в виде секунд дня (```3600 * часов + 60 * минут```) для запуска/остановки времения. Время, которое виджет отправляет оборудованию, является локальным временем пользователя.
Индексы по выбранных дней:

```
Понедельник - 1
Вторник - 2
...
Суббота - 6
Воскресенье - 7
```

You can also change state of widget on UI. See below sketches.
Вы также можете изменить состояние виджета в интерфейсе пользователя. Смотрите ниже примеры кода.

**Пример кода:** [Простой Ввод времени для времени начала](https://github.com/blynkkk/blynk-library/blob/master/examples/Widgets/TimeInput/SimpleTimeInput/SimpleTimeInput.ino)

**Пример кода:** [Расширенный Ввод времени](https://github.com/blynkkk/blynk-library/blob/master/examples/Widgets/TimeInput/AdvancedTimeInput/AdvancedTimeInput.ino)

**Пример кода:** [Обновление Ввода времени в пользовательском интерфейсе](https://github.com/blynkkk/blynk-library/blob/master/examples/Widgets/TimeInput/UpdateTimeInputState/UpdateTimeInputState.ino)
