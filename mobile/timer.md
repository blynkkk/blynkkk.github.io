
### Timer

Timer triggers actions at a specific time. Even if smartphone is offline. By default start time sends 1 (HIGH), 
stop time sends 0 (LOW). You can change this with any other values.
Recent Android version also has improved Timer within Eventor widget.
With Eventor Time Event you can assign multiple timers on same pin, send any string/number, select days and timezone. 
It is recommended to use Eventor over Timer widget.
However Timer widget is still suitable for simple timer events.

**NOTE:** The timer widget rely on the server time and not your phone time. Sometimes the phone time may not match the server time. 

**Sketch:** [Timer](https://github.com/blynkkk/blynk-library/blob/master/examples/Widgets/Timer/Timer.ino)