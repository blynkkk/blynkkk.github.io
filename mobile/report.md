
### Reporting widget

The reporting widget is designed like a button, so you can open the different settings in the edit mode and the run mode.
It is done in that way, so end users (within published apps) could setup the reports without edit mode.

#### Edit mode

In the edit mode (the project is stopped) you need to define the datastreams you would like to see in your reports.
At the moment, the reporting widget designed to work with the Device Tiles widget.
However, in case you don't have the Device Tiles widget, you still can select the single device or
the group of devices as a target for your report and the datastreams for them.

At the moment you can't use both. You have to choose either Device Tiles or single / group of the devices for the report.

#### Run mode

After you did setup of the datastreams you are ready to run your report! To do that - you need to run the project
and click on reports widget within your project layout.

### Report settings

Every report has a bunch of the settings:

```Report name``` - for every new report you need to provide a name, obvious.

```Data source``` - select the datastreams you setup in edit mode for which you want to see the report.

```Report Frequency``` - This field defines a period of your report. It could ```one-time``` report (sends data right away when you
click on the report icon). It could be periodic ```daily```/```weekly```/```monthly``` report.
Every periodic report has a specific trigger time in a field called ```At Time``` and ```Start```/```End``` dates for your report.
In addition, for weekly report you can select required day of the week (```SUN```, ```MON```, etc) and for the monthly report you
can select either the first day of the month or the last day of the month.

```Recipients``` - field allows you to specify report receivers. Up to 5 recipients.

```Data resolution``` - defines granularity of your reports. Right now we support ```minute```, ```hourly``` and ```daily``` granularity.
For example, when you generate daily report with 1 minute granularity you'll get ```24 * 60 * 60```
points in your daily report for every selected datastream.

```Group data in reports``` - field allows you to specify the output format of the CSV files. For example, with ```By Datastream```
option you will receive one file for the every selected datastream. So if you have 10 devices with 2 datastreams you'll get 20
csv files as output of the report. With ```By Device``` option you'll get 2 files, 1 for the every device.

```Timezone correction``` - allows you select the specific timezone for your data so you'll always get data in relative to you timezone.

```Date and time format``` - defines format of timestamp field of your data. You can select ```2018-06-21 20:16:48```,
```2018-06-21T20:16:48+03:00``` or other supported formats. There is one specific ```Timestamp``` format - that is the difference,
measured in milliseconds, between the current time and midnight, January 1, 1970 UTC.

After your report is done - click on "OK" button at the right upper corner. Your report is ready!

Now, if everything was fine - you'll see ```Next``` label under your report that identifies exactly trigger time of your report.
After the report is executed you'll see ```Last``` label under the report that identifies the last execution time of your report.

The ```Last``` label also contains the status regarding your report. It could be ```OK``` (the report is generated and sent to the Recipients),
```No Data``` (the report doesn't have any data for the selected period) or ```Error``` (something went wrong,
in that case please contact the Blynk Team support).

Reports don't require the project to be active in order to be executed. However, have in mind that non-active project do not generate any data.


