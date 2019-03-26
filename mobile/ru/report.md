
### Отчеты (Reports)

Функция виджета «Отчеты» заключается в настройке и разметке отчетов данных в формате CSV. Вы можете выбрать разовые или непрерывные запланированные отчеты.

Кроме того, в отчетах вы можете очистить все пользовательсике данные, собранные с ваших устройств.

Вам необходимо настроить начальные параметры в режиме редактирования, а затем уже в режиме воспроизведения вы сможете настроить сами отчеты.

#### Режим редактирования. Конфигурация ввода данных

In edit mode (when your project is stopped) you define the Datastreams you would like to later be included in reports.
Reports widget is  designed to work with the Device Tiles widget. If you don't use Device Tiles you can still select a single device or a group of devices as a source of data for reports.

You have to choose either Device Tiles or single / group of the devices for the report. You can't combine these 2 options.

В режиме редактирования (когда ваш проект остановлен) вы определяете потоки данных, которые вы хотели бы позже включить в отчет.
Виджет «Отчеты» предназначен для работы с виджетом «Плитка устройств» (Device Tiles). Если вы не используете плитки устройств, вы все равно можете выбрать одно устройство или группу устройств в качестве источника данных для отчетов.

Вы должны выбрать либо Плитка устройств, либо одино устройство либо группа устройств для отчета. Вы не можете объединить эти оба варианта.

#### Режим воспроизведения 

После добавления исходных устройств и их потоков данных нажмите кнопку «Воспроизвести» и нажмите кнопку «Отчеты».

### Настройка отчетов

Каждый параметр отчета предполагает свои собственные настройки:

```Report name``` (имя отчета) -  дайте вашему отчету осмысленное имя.

```Data source``` (источники данных) - выберите потоки данных, которые вы хотели бы включить в отчеты.

```Report Frequency``` (периодичность отчетов) -  Определяет, как часто будут отправляться отчеты. Они могут быть разовыми и запланированными.

```one-time``` (Сейчас) -  мгновенно сформирует отчет и отправит его на указанные адреса электронной почты. Нажмите на значок справа, чтобы отправить отчет.

Запланированные отчеты могут быть отправлены ```daily```/```weekly```/```monthly``` (ежедневно/еженедельно/ежемесячно).

 ```At Time``` (Время)  установите время дня, когда отчет будет отправлен.
 ```Start```/```End``` (Качало/Конец) указывает дату начала и окончания оправки отчетов.

Для еженедельного отчета вы можете выбрать день недели, когда отчет должен быть отправлен.
Для ежемесячного отчета вы можете выбрать, отправку отчета в первый или последний день месяца.

```Recipients``` (Получатели) -  укажите до 5 адресов электронной почты..

```Data resolution``` (Разрешение данных) определяет детализацию ваших отчетов.  Поддерживаемые детализации: ```minute``` (ежеминутно), ```hourly``` (ежечасно) и ```daily``` (ежедневно).
Например, когда вы генерируете ежедневный отчет с детализацией в 1 минуту, вы получаете ```24 * 60 * 60``` единиц данных в вашем ежедневном отчете за каждый выбранный поток.

```Group data in reports by``` (Группировка данных в отчетах) -  укажите выходной формат файла-(ов) CSV:

```Datastream``` (Поток) - вы получите один CSV файл для каждого потока данных.

```Device``` (Устройство) - вы получите один CSV-файл на каждое устройство. Каждый файл будет содержать все включенные потоки данных.

```Report``` (Отчет) - вы получите один CSV-файл для всех ваших устройств и всех ваших потоков данных.

```Timezone correction``` (Времненная зона) -  укажите корректировку часового пояса, если вам нужно настроить дату и время отчета на определенный часовой пояс.

```Date and time format``` (Формат даты и времени) -  определяет формат поля временной метки ваших данных.
Вы можете выбрать ```2018-06-21 20:16:48```, ```2018-06-21T20:16:48+03:00``` или другой поддерживаемы формат.

There is one specific ```Timestamp``` format - which reflects the difference between the current time and midnight, January 1, 1970 UTC measured in milliseconds.

After the report is set up - click on "OK" button at the right upper corner. Your report is ready.


Once you configured the report you will see when is the ```Next``` report scheduled and also a schedule for this report.

After the report was sent at least once, you can see when the ```Last``` report was sent.

```Last``` label also contains the status regarding the report:

- ```OK```: the report was generated and sent to the Recipients successfully;
- ```No Data```: the report doesn't contain any data for the configured period;
- ```Error```: something went wrong. Please contact the Blynk Team support;

Reports will be generated even if your project is not in active (Play) mode. However, inactive projects don't generate any data.

**NOTE:** all reports are encoded in UTF-16. Please, make sure you selected UTF-16 as required "Character set" for your csv reader.


