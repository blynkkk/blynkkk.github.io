
### Терминал (Terminal)

Displays data from your hardware. Allows to send any string to your hardware. Terminal always stores last 25 messages
your hardware had send to Blynk Cloud. This limit may be increased on Local Server with ```terminal.strings.pool.size``` 
property.

You can use special commands with this widget:

Отображает данные с вашего оборудования. Позволяет отправить любую строку с вашего оборудования. Терминал всегда хранит последние 25 сообщений, которые ваше оборудование отправило в Blynk. Этот ограничение может быть увеличено в настройках локального сервера с помощью параметра ```terminal.strings.pool.size```.

С этим виджетом Вы можете использовать специальные команды:

```cpp
// Печатает значения, как Serial.print
terminal.print();   
// Печатает значения, как Serial.println()
terminal.println();
// Записать необработанные данные в буффер
terminal.write();
// Убедится, что все данные были отправлены с устройства в терминал
terminal.flush();
// Стереть все данные в терминале
terminal.clear();
```

**Пример кода:** [Терминал](https://github.com/blynkkk/blynk-library/blob/master/examples/Widgets/Terminal/Terminal.ino)
