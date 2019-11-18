### Data Stream value invalidation

Some data streams have meaningful value only when it is fresh (updated recently). 
For such data streams you can setup the invalidation period and invalidate the value according to the selected policy. 

For example, you made an thermometer and interested in the current temperature outside the window. 
Thermometer wakes up hourly and sends the current temperature to the display widget on the web or mobile. 
Let's assume you made a setup with the 2 hours invalidation period and selected ```No Data``` policy.

Due to any malfunction your device could stop sending the updates. 
Without the invalidation period you will always see the latest value on the screen. 
However, with invalidation period after 2 hours since the last update - value will be invalidated 
with ```No Data``` label. So end users will not be confused with the "freezed latest value".

Currently you can select one of the following invalidation policies:

- Nothing - widget will be empty and will show nothing
- Default - widget will be filled with the default value of the data stream if it is present
- No Data - text ```No Data``` will be showed
- Empty - text ```Empty``` will be showed
- -- - text ```--``` will be showed