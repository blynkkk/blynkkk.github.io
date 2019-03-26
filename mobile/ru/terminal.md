
### Terminal

Displays data from your hardware. Allows to send any string to your hardware. Terminal always stores last 25 messages
your hardware had send to Blynk Cloud. This limit may be increased on Local Server with ```terminal.strings.pool.size``` 
property.

You can use special commands with this widget:

```cpp
// Print values, like Serial.print
terminal.print();   
// Print values, like Serial.println()
terminal.println();
 // Write a raw data buffer
terminal.write();
// Ensure that data was sent out of device
terminal.flush();
// Erase all values in the terminal
terminal.clear();
```

**Sketch:** [Terminal](https://github.com/blynkkk/blynk-library/blob/master/examples/Widgets/Terminal/Terminal.ino)