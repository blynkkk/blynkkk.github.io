# Аппаратные настройки

## Arduino через USB \(без расширительных плат\)

Если у вас нет расширительной платы и ваше оборудование не имеет подключения к сети, вы все равно можете использовать Blynk - напрямую через USB:

1. Откройте [Arduino Serial USB пример](https://github.com/blynkkk/blynk-library/blob/master/examples/Boards_USB_Serial/Arduino_Serial_USB/Arduino_Serial_USB.ino) и замените [Auth Token](../#getting-started-getting-started-with-application-4-auth-token)

```cpp
// Вы можете использовать запасной аппаратный серийный порт на платах, которые его имеют (например, Mega)
#include <SoftwareSerial.h>
SoftwareSerial DebugSerial(2, 3); // RX, TX

#define BLYNK_PRINT DebugSerial
#include <BlynkSimpleStream.h>

// Вы должны получить Auth Token в приложении Blynk.
// Перейдите в настройки проекта (значок гайки).
char auth[] = "YourAuthToken";

void setup()
{
  // Debug console
  DebugSerial.begin(9600);

  // Blynk will work through Serial
  Serial.begin(9600);
  Blynk.begin(auth, Serial);
}

void loop()
{
  Blynk.run();
}
```

1. Запустите скрипт, который обычно находится в папке `/scripts`:
   * Windows:`My Documents\Arduino\libraries\Blynk\scripts`
   * Mac    `User$/Documents/Arduino/libraries/Blynk/scripts`

**На Windows:**

Откройте командную строку cmd.exe

Задайте свой путь к папке blynk-ser.bat. Например:

```text
cd C:\blynk-library-0.3.1\blynk-library-0.3.1\scripts
```

Run `blynk-ser.bat` file. For example : `blynk-ser.bat -c COM4` \(where COM4 is port with your Arduino\) Запустите файл `blynk-ser.bat`. Например: `blynk-ser.bat -c COM4` \(где COM4 - порт с вашим Arduino\)

И нажмите «Ввод», нажмите «Ввод» и нажмите «Ввод»...

**На Linux и Mac**:

Перейдите в папку `/scripts.` Например:

```text
cd User$/Documents/Arduino/libraries/Blynk/scripts
```

Когда окажетесь внутри этой папки, запустите:

```text
user:scripts User$ ./blynk-ser.sh
```

**Предупреждение:** Не закрывайте окно терминала с запущенным скриптом.

В некоторых случаях вам также может потребоваться выполнить:

```text
user:scripts User$ chmod +x blynk-ser.sh
```

Вам также может понадобиться запустить скрипт с функцией `sudo`

```text
user:scripts User$ sudo ./blynk-ser.sh
```

Вот что вы увидите в приложении Terminal на Mac \(адрес usbmodem может быть другим\):

```text
[ Press Ctrl+C to exit ]
/dev/tty.usbmodem not found.
Select serial port [ /dev/tty.usbmodem1451 ]:
```

Скопируйте адрес последовательного порта: `/dev/ tty.usbmodem1451` и вставьте его обратно:

```text
Select serial port [ /dev/tty.usbmodem1451 ]: /dev/tty.usbmodem1451
```

После того, как вы нажмете Enter, вы увидите текст, похожий на этот:

```text
Resetting device /dev/tty.usbmodem1451...
Connecting: GOPEN:/dev/tty.usbmodem1451,raw,echo=0,clocal=1,cs8,nonblock=1,ixoff=0,ixon=0,ispeed=9600,ospeed=9600,crtscts=0 <-> openssl-connect:blynk-cloud.com:9443,cafile=/Users/.../server.crt,nodelay
2015/10/03 00:29:45 socat[30438.2046857984] N opening character device "/dev/tty.usbmodem1451" for reading and writing
2015/10/03 00:29:45 socat[30438.2046857984] N opening connection to LEN=16 AF=2 45.55.195.102:9443
2015/10/03 00:29:45 socat[30438.2046857984] N successfully connected from local address LEN=16 AF=2 192.168.0.2:56821
2015/10/03 00:29:45 socat[30438.2046857984] N SSL connection using AES128-SHA
2015/10/03 00:29:45 socat[30438.2046857984] N starting data transfer loop with FDs [3,3] and [4,4]
```

**ПРИМЕЧАНИЕ:** Arduino IDE может жаловаться на то, что «программа не отвечает». Вам необходимо прекратить выполнение скрипта перед загрузкой нового скейтча.

**Дополнительные материалы:**

* [Учебник: Управление Arduino через USB с приложением Blynk. Плата Ethernet не требуется. Mac OS](https://www.youtube.com/watch?v=fgzvoan_3_w)
* [Как управлять Arduino \(без проводов\) с помощью blynk через USB. Windows](https://www.youtube.com/watch?v=I_hgIj2FdPI)
* [Учебные пособия: управление Arduino с помощью Blynk через USB](http://www.instructables.com/id/Control-arduino-using-Blynk-over-usb/)

## Raspberry Pi

1. Подключите Raspberry Pi к Интернету и откройте его консоль.
2. Запустите эту команду \(она обновляет ваш репозиторий пакетов операционной системы, чтобы добавить необходимые пакеты\):

   ```text
    curl -sL "https://deb.nodesource.com/setup_6.x" | sudo -E bash -
   ```

3. Загрузите и соберите библиотеку Blynk JS, используя npm:

   ```text
    sudo apt-get update && sudo apt-get upgrade
    sudo apt-get install build-essential
    sudo apt-get install -g npm 
    sudo npm install -g onoff
    sudo npm install -g blynk-library
   ```

4. Запустите тестовый скрипт Blynk \(поставьте свой ключ авторизации\):

   ```text
    blynk-client 715f8cafe95f4a91bae319d0376caa8c
   ```

5. Вы можете написать свой собственный скрипт на основе [примеров](https://github.com/vshymanskyy/blynk-library-js/tree/master/examples)
6. Чтобы включить автоматический перезапуск Blynk для Pi, найдите файл `/etc/rc.local` и добавьте туда:

   ```text
    node full_path_to_your_script.js <Auth Token>
   ```

**Дополнительные материалы:**

* [Учебные пособия: Blynk на Javascript для Raspberry Pi, Intel Edison и другие](http://www.instructables.com/id/Blynk-JavaScript-in-20-minutes-Raspberry-Pi-Edison)
* [Учебные пособия: использование датчиков DHT11/DHT12 с Raspberry Pi и Blynk](http://www.instructables.com/id/Raspberry-Pi-Nodejs-Blynk-App-DHT11DHT22AM2302/?ALLSTEPS)

**Примечание:** Вместо использования Node.js вы также можете создать версию библиотеки C++ \(такую же, как для Arduino, на основе WiringPi\):

* [Библиотека README для Linux](https://github.com/blynkkk/blynk-library/blob/master/linux/README.md)
* [Тема сообщества Blynk: How-To Raspberry Pi](https://community.blynk.cc/t/howto-for-raspberry-pi/332)
* [Видеоурок - Настройка Blynk и Raspberry Pi](https://www.youtube.com/watch?v=iSG_8g6KyGE)

## Беспроводной ESP8266

Вы можете запустить Blynk прямо на ESP8266!

Установите последнюю версию библиотеки ESP8266 для Arduino, используя [это руководство](https://github.com/esp8266/Arduino#installing-with-boards-manager).

**Пример кода:** [ESP8266\_Standalone](https://github.com/blynkkk/blynk-library/blob/master/examples/Boards_WiFi/ESP8266_Standalone/ESP8266_Standalone.ino)

**Дополнительные материалы:**

* [Учебные пособия: ESP8266 ESP-12 \(Беспроводной\) + Blynk](http://www.instructables.com/id/ESP8266-ESP-12Standalone-Blynk-101)
* [Учебные пособия: ESP8266-12 \(Беспроводной\) датчик температуры lm35 + Blynk](http://www.instructables.com/id/ESP8266-12-blynk-wireless-temperature-LM35-sensor/?ALLSTEPS)
* [Пошаговое руководство на русском языке](http://esp8266.ru/esp8266-blynk)

## NodeMCU

Пожалуйста, следуйте [этой подробной инструкции](https://github.com/blynkkk/blynk-library/tree/master/examples/Boards_WiFi/NodeMCU#instruction-for-nodemcu-setup). Или посмотрите [этот видеоурок](https://www.youtube.com/watch?v=FhS44hGk1Lc).

## Arduino + ESP8266 WiFi с AT командами

Этот тип подключения не рекомендуется для начинающих. Если вы хотите попробовать, пожалуйста, внимательно прочитайте [этот раздел справки](http://help.blynk.cc/hardware-and-libraries/arduino/esp8266-with-at-firmware)

**Примечание:** Некоторые платы, такие как Arduino UNO WiFi от Arduino.org, не используют AT-команды \(и не предоставляют соответствующих библиотек\), поэтому это делает их непригодными для использования с Blynk.

## Particle

Blynk работает со всем семейством продуктов Particle: Core, Photon и Electron.

1. Открыть [Particle Web IDE](https://build.particle.io/build). Требуется регистрация.
2. Идем в библиотеки.
3. Найдите  **Blynk**  в общих библиотеках и нажмите на него.
4. Откройте пример `01_PARTICLE.INO`.
5. Нажмите «использовать этот пример» \(use this example\).
6. Поместите свой токен здесь: `char auth [] ="YourAuthToken";` и прошейте Particle!

Вы можете отсканировать этот QR-код из приложения Blynk, и вы получите готовый к тесту проект для **Particle Photon**. Просто вставьте свой токен ключ в пример `01_PARTICLE.INO`.

![](../.gitbook/assets/Particle%20Demo1530733075.png)

**Дополнительные материалы:**

* [Ядро Particle + DHT22](https://www.hackster.io/gusgonnet/temperature-humidity-monitor-with-blynk-7faa51)

