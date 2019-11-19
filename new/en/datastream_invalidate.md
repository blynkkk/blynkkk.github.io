### Datastream: Invalidate Value

Use this setting to manage the *freshness* of the data. When enabled, server will automatically check the timestamp of the latest value and act accordingly to settings.


**Invalidate in:** 
Specifies the time period in seconds, minutes or hours when data is considered fresh.

**then set:** 
Specifies what to do when data is no longer fresh. You have such options: 

| Option  | How it works                                            |
|---------|--------------------------------------------------------|
| Nothing | The latest value will be shown in the apps             |
| Default | Will show `Default` value (check Settings) in the apps |
| No Data | Will show "No Data" placeholder in the apps            |
| Empty   | Will show nothing in the apps                          |
| --      | Will show dashes `--` in the apps                      |



Example: 
1. A temperature datastream is set to `Invalidate in 1 hour, then set to "--"`
2. It's 4:00 PM now and the latest value of `3.14ºC` was received at 3:30 PM. Data is considered to be fresh and any widget will display it. 
3. It's 5:00 PM, and there was no new data since 3:30 PM (maybe device is no longer working). A temperature widget in the app will show `--` because data is no longer fresh.
