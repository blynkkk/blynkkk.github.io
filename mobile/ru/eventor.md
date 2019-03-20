
### Eventor

Eventor widget allows you to create simple behaviour rules or **events**. 
Let's look at a typical use case: read temperature from DHT sensor and send push notification when the temperature is over a certain limit :  
 
```cpp
  float t = dht.readTemperature();
  if (isnan(t)) {
    return;
  }
  if (t > 40) {
    Blynk.notify(String("Temperature is too high : ") + t);
  }
```

With Eventor you don't need to write this code. All you need is to send the value from the sensor to the server :

```cpp
  float t = dht.readTemperature();
  Blynk.virtualWrite(V0, t);
```
Don't forget that ```virtualWrite``` commands should be wrapped in the timer and can't be used in the main loop.

**NOTE** Don't forget to add notification widget.

Eventor comes handy when you need to change conditions on the fly without re-uploading new sketch on 
the hardware. You can create as many **events** as you need.
Eventor also could be triggered from the application side. You just need to assign the widget to the same pin as your Event within Eventor.
Eventor doesn't constantly sends events. Let's consider simple event as above ```if (temperature > 40) send notification ```.
When temperature goes beyond 40 threshold - notification action is triggered. If temperature continues to stay above the 
40 threshold no actions will be triggered. But if ```temperature``` goes below threshold and then passes it again -
notification will be sent again (there is no 5 sec limit on Eventor notifications).
 
Eventor also supports Timer events. For example, you can set a pin ```V1``` ON/HIGH at 21:00:00 every Friday.
With Eventor Time Event you can assign multiple timers on same pin, send any string/number, select days and timezone.

In order to remove created **event** please use swipe. You can also swipe out last element in the Event itself. 

**Sketch:** [Eventor](https://github.com/blynkkk/blynk-library/blob/master/examples/Widgets/Eventor/Eventor.ino)


**NOTE:** The timer widget rely on the server time and not your phone time. Sometimes the phone time may not match the server time. 
**NOTE** : Events are triggered only once when the condition is met. That's mean 
[chaining of events](https://community.blynk.cc/t/eventor-behavior-bug-feature/20962) is not possible (however, could be enabled for commercials).
