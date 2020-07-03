# Value Display

Displays incoming data from your sensors or Virtual Pins. Can work in 2 modes :

* PUSH mode \(select it from Frequency Reading picker\);
* Frequency Reading mode;

In PUSH mode you update value display from hardware side with code :

```cpp
Blynk.virtualWrite(V1, val);
```

In this mode every message that hardware sends to server is stored automatically on server. PUSH mode doesn't require application to be online or opened.

With Frequency Reading mode you need to select update interval and application will trigger events with required timing. Your application should be open and running in order to make requests to hardware. You don't need any code for Analog and Digital pins in that case. However for virtual pins you need to use next code :

```cpp
//triggered from app
BLYNK_READ(V1)
{
  //send to app
  Blynk.virtualWrite(V1, val);
}
```

## Home Screen Value Display

You can also add Value Display to your Android Home Screen. Value Display works via HTTPS in that case. Have in mind that in "Home Screen" mode Value Display has few limitations. Value Display will update it's state only once per 15 min. You can change this via Widget Settings. However update interval less than 15 minutes is not guaranteed.  
You can also resize Value Display on Home Screen - just do long click on widget and resize it as you need.

**Note :** Adding home screen widget costs 100 energy. This energy not rechargeable. **Note :** Home Screen Widgets for Local Blynk servers requires port 8080 to be opened.

**Sketch:** [BlynkBlink](https://github.com/blynkkk/blynk-library/blob/master/examples/GettingStarted/BlynkBlink/BlynkBlink.ino)

