
### Graph

Easily plot incoming data from your project in various designs. You can also scroll and zoom graph.

Can work in 2 modes : 

- PUSH mode (select if from Frequency Reading picker);
- Frequency Reading mode;

In PUSH mode you update gauge from hardware side with code : 
 
```cpp
Blynk.virtualWrite(V1, val); 
```

In this mode every message that hardware sends to server is stored automatically on server. PUSH mode doesn't require 
application to be online or opened.

With Frequency Reading mode you need to select update interval and application will trigger events with required timing. 
Your application should be open and running in order to make requests to hardware. You don't need any code for Analog and 
digital pins in that case. However for virtual pins you need to use next code : 

```cpp
//triggered from app
BLYNK_READ(V1)
{
  //send to app
  Blynk.virtualWrite(V1, val);
}
```

**Sketch:** [BlynkBlink](https://github.com/blynkkk/blynk-library/blob/master/examples/GettingStarted/BlynkBlink/BlynkBlink.ino)