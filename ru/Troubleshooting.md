# Решение проблем

## Соединение

Если у вас возникли проблемы с подключением, выполните следующие действия:

1. Убедитесь, что ваше оборудование, провода, кабели и блок питания находятся в исправном состоянии, не повреждены и т.д.      
   Используйте качественные USB-кабели и USB-порты.
2. Проверьте проводку, используя примеры (клиент TCP/HTTP или аналогичный), **прилагаемые к вашему оборудованию**.
   * Как только вы поймете, как управлять соединением, использовать Blynk станет намного проще.
3. Попробуйте запустить команду ```telnet blynk-cloud.com 80``` со своего ПК, подключенного к той же сети, что и ваше оборудование. Вы должны увидеть что-то вроде: ```Подключено к blynk-cloud.com```.
4. Попробуйте запустить примеры Blynk по умолчанию для вашей платформы **без изменений**, чтобы увидеть, работают ли они.
   * Дважды проверьте, что вы выбрали **правильный пример** для вашего типа подключения и модели оборудования.
   * Наши примеры содержат **комментарии и объяснения**. **Читайте их внимательно.**
   * Убедитесь, что ваш токен авторизации действителен (скопирован из приложения и **не содержит пробелов и т.п.**)
   * Если это не работает, попробуйте заглянуть в [печать отладочной информации в порт](/#enable-debug).
5. Готово! Добавьте свои модификации и функциональность. Наслаждайтесь Blynk!

**Примечание:** Если к вашей сети подключено несколько устройств, все они должны иметь разные MAC и IP-адреса. Например, при использовании двух Arduino UNO с Ethernet расширениями, пример по умолчанию для обоих из них вызовет проблемы с подключением. Вам следует использовать пример [ручная настройка Ethernet](https://github.com/blynkkk/blynk-library/blob/master/examples/Boards_Ethernet/Arduino_Ethernet_Manual/Arduino_Ethernet_Manual.ino).

## Подключение к сети WiFi
Если у вас возникли проблемы с подключением по WiFi, пожалуйста, проверьте следующие ошибки:

* You're trying to connect to "WPA & WPA2 Enterprise" network (often used in offices), and your shield does not support this security method
* Your WiFi network has a login page that requests entering an access token (often used in restaurants)
* Your WiFi network security disallows connecting alien devices completely (MAC filtering, etc)
* There is a firewall running. Default port for hardware connections is 80 (8080 on the Local Server).
Make sure it's open.

* Вы пытаетесь подключиться к сети 'WPA & WPA2 Enterprise' (часто используется в офисах), а ваш шилд не поддерживает этот метод шифрования
* В вашей WiFi-сети есть страница входа, которая запрашивает ввод ключа доступа (часто используется в ресторанах)
* Безопасность вашей сети Wi-Fi запрещает полное подключение чужих устройств (фильтрация MAC-адресов и т.п.)
* Работает Брандмауэр. Порт по умолчанию для аппаратных подключений - 80 (8080 на локальном сервере). Убедитесь, что он открыт.  

## Задержки (Delay)

If you use long ```delay()``` or send your hardware to sleep inside of the ```loop()``` expect connection drops and downgraded performance.

***DON'T DO THAT:***
```cpp
void loop()
{
  ...
  delay(1000); // this is long delay, that should be avoided
  other_long_operation();
  ...
  Blynk.run();
}
```

***Note:*** This also applies to the BLYNK_READ & BLYNK_WRITE handlers!

***SOLUTION:***
If you need to perform actions in time intervals - use timers, for example [BlynkTimer](/#blynk-firmware-blynktimer).

## Flood Error

If your code frequently sends a lot of requests to our server, your hardware will be disconnected. Blynk App may show "Your hardware is offline"

When ```Blynk.virtualWrite``` is in the ```void loop```, it generates hundreds of "writes" per second 

Here is an example of what may cause flood. ***DON'T DO THAT:***
```cpp
void loop()
{
  Blynk.virtualWrite(1, value); // This line sends hundreds of messages to Blynk server
  Blynk.run();
}
```

***SOLUTION:***
If you need to perform actions in time intervals - use timers, for example [BlynkTimer](/#blynk-firmware-blynktimer).

Using ```delay()``` will not solve the problem either. It may cause [another issue](/#delay). Use timers!

If sending hundreds of requests is what you need for your product you may increase flood limit on local server 
and within Blynk library.
For local server you need to change ```user.message.quota.limit``` property within ```server.properties``` file :

        #100 Req/sec rate limit per user.
        user.message.quota.limit=100
        
For library you need to change ```BLYNK_MSG_LIMIT``` property within ```BlynkConfig.h``` file :
 
        //Limit the amount of outgoing commands.
        #define BLYNK_MSG_LIMIT 20

## Enable debug

To enable debug prints on the default Serial, add this on the top of your sketch **(it should be the first line
in your sketch)**:

```cpp
#define BLYNK_DEBUG // Optional, this enables lots of prints
#define BLYNK_PRINT Serial
```
And enable serial in ```void setup()```:

```cpp
Serial.begin(9600);
```

You can also use spare Hardware serial ports or SoftwareSerial for debug output (you will need an adapter to connect to it with your PC).

***Note:*** enabling debug mode will slow down your hardware processing speed up to 10 times.

## Geo DNS problem

Geo DNS issue is no longer a problem. It was solved in 2017.

## Reset password

On login screen click on "Forgot password?" label and than type your email and ```Send``` button.
You'll get instruction on your email.

### Android reset password flow

1. Open instruction email **from your smartphone or tablet**;
2. Click on "Reset now" button in your email;
3. Click on Blynk icon in below popup and reset the pass:

<img src="images/reset.png"/>
