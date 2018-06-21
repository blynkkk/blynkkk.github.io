
### Reporting widget

Reporting widget is designed like a button, so you can open different settings in the edit mode and the run mode.
It is done in that way, so end users (within published apps) could setup reports without edit mode.

#### Edit mode

In edit mode (project is stopped) you need to define the datastreams you would like to see in your reports.
At the moment, reporting widget designed to work with the Device Tiles widget.
However, in case you don't have Device Tiles widget in your project, you still can select single device or
group of devices as a target for your report and datastreams for them.
At the moment you can't use both: the Device Tiles and single device for the report.

#### Run mode

After you did setup of the datastreams you are ready to run your report! To do that you need to run the project
and click on reports widget within your project layout. Now you can add as many reports as you want.

### Report settings

**Report name** - for every new report you need to provide a name.
**Data source** - select datastreams/sources that you setup in edit mode during the widget creation.
**Report Frequency** - This field defines a period of your report. It could **one-time** report (sends data right away when you
click on the report icon). It could be periodic **daily**/**weekly**/**monthly** report.
Every periodic report has a specific trigger time in a field called **At Time** and Start/End date for your report.
In addition, for weekly report you can select required day of the week (sun, mon, etc) and for monthly report you
can select either first day of the month or last day of the month.
**Recipients** - field allows you to specify report receivers.
**Data resolution** - defines granularity of your reports. Right now we support minute, hour and day granularity.
For example, when you generate daily report with 1 minute granularity you'll get 24 * 60 * 60 points in your daily report.
**Group data in reports** - field allows you to specify output format of the CSV files. For example, with "By Datastream"
option you will receive one file for every selected datastream. So if you have 10 devices with 2 datastreams you'll get 20
csv files as output of the report. With "By Device" option you'll get only 2 files, 1 for every device.
**Timezone correction** - allows you select the specific timezone for your data so you'll always get data in your local timezone.
**Date and time format** - defines format of timestamp field of your data. You can select "2018-06-21 20:16:48",
"2018-06-21T20:16:48+03:00" or other supported formats. There is one specific **Timestamp** format - that is the difference,
measured in milliseconds, between the current time and midnight, January 1, 1970 UTC.

After your report is done click on "OK" button at the right upper corner. Your report is ready!
Now if everything was fine - you'll see "Next" label under your report that identified exactly trigger time of your report.
After report is executed you'll see "Last" label under the report that identifies last execution time of your report.
"Last" label also contains status regarding your report. It could be OK (report is generated and sent to the Recipients),
No Data (report doesn't have any data for selected period and datastreams) or Error (something went wrong, in case we do recommend
to contact Blynk Team support).

Reports don't require project to be active in order to be executed. However, have in mind that non-active project do not generate any data.


