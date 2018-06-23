
### Reports Widget

Function of Reports is to configure and customize data reports in CSV format. You can choose between one-time or continuous scheduled reports.

Also, within the Reports you can clear all the data collected by your devices. 

You need to configure initial inputs in Edit mode, and then, in Play mode you will be able to customize reports. 

#### Edit mode. Data inputs configuration

In edit mode (when your project is stopped) you define the Datastreams you would like to later be included in reports.
Reports widget is  designed to work with the Device Tiles widget. If you don't use Device Tiles you can still select a single device or a group of devices as a source of data for reports.

You have to choose either Device Tiles or single / group of the devices for the report. You can't combine these 2 options.

#### Play mode. 

After you added source devices and their Datastreams click Play button and click on the Reports button. 

### Customizing Reports.

Every Report option supposes it's own settings:

```Report name``` - give your report a meaningful name.

```Data source``` - select the Datastreams you would like to be included in reports.

```Report Frequency``` - Defines how often reports will be sent. They can be one-time and scheduled.
```one-time``` - will instantly generate report and send it to the email addresses specified. Click on the right icon to send it.

Scheduled reports can be sent ```daily```/```weekly```/```monthly```.

 ```At Time``` will set up a time of the day the report will be sent. 
 ```Start```/```End``` specifies start and end date the reports will continue to be sent. 

For Weekly Report you can select a day of the week when report should be sent.
For Monthly report you can choose whether to send report on the first or last day of the month.

```Recipients``` - specify up to 5 email addresses.

```Data resolution``` defines granularity of your reports. Supported granularities are: ```minute```, ```hourly``` and ```daily```.
For example, when you generate daily report with 1 minute granularity you'll get ```24 * 60 * 60```
points in your daily report for every selected Datastream.

```Group data in reports``` -  specify the output format of the CSV file(s).

```By Datastream``` you will get 1 CSV file for each Datastream.

```By Device``` you will get 1 CSV file per each device. Each file will contain all of the included Datastreams.

```Timezone correction``` - specify the time zone adjustment if you need to get report date and time adjusted to a specific time zone

```Date and time format``` - defines the format of the timestamp field of your data. You can select ```2018-06-21 20:16:48```,
```2018-06-21T20:16:48+03:00``` or other supported formats.

There is one specific ```Timestamp``` format - which reflects the difference between the current time and midnight, January 1, 1970 UTC measured in milliseconds.

After the report is set up - click on "OK" button at the right upper corner. Your report is ready.


Once you configured the report you will see when is the ```Next``` report scheduled and also a schedule for this report.

After the report was sent at least once, you can see when the ```Last``` report was sent.

```Last``` label also contains the status regarding the report. 
- ```OK```: the report was generated and sent to the Recipients successfully;
- ```No Data```: the report doesn't contain any data for the configured period;
- ```Error```: something went wrong. Please contact the Blynk Team support;

Reports will be generated even if your project is not in active (Play) mode. However, inactive projects don't generate any data.


