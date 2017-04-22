
### Level Display

Displays incoming data from your sensors or Virtual Pins. Level Display is very similar to progress bar, it is very nice 
and fancy view for indication of "filled" events, like "level of battery". 
You can update value display from hardware side with code : 
 
```cpp
Blynk.virtualWrite(V1, val); 
```

Every message that hardware sends to server is stored automatically on server. PUSH mode doesn't require 
application to be online or opened.

**Sketch:** [Push Example](https://github.com/blynkkk/blynk-library/blob/master/examples/GettingStarted/PushData/PushData.ino)