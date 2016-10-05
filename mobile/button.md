
### Button

Works in push or switch modes. Allows to send 0/1 (LOW/HIGH) values. Button sends 1 (HIGH) on press and sends 0 (LOW) on release.

You can change button state from hardware side. For example, turn on button assigned to virtual pin V1 : 

```Blynk.virtualWrite(V1, HIGH)```

You can change button labels from hardware with : 

```Blynk.virtualWrite(V1, "onLabel", "ON");```

```Blynk.virtualWrite(V1, "offLabel", "OFF");```

or change color : 

```
Blynk.virtualWrite(V1, "color", "#D3435C"); //#D3435C - Blynk RED 
```

**Sketch:** [Basic Sketch](https://github.com/blynkkk/blynk-library/blob/master/examples/GettingStarted/BlynkBlink/BlynkBlink.ino)

**Sketch:** [Physical Button Interrupt](https://github.com/blynkkk/blynk-library/blob/master/examples/More/Sync/ButtonInterrupt/ButtonInterrupt.ino)

**Sketch:** [Physical Button Poll](https://github.com/blynkkk/blynk-library/blob/master/examples/More/Sync/ButtonPoll/ButtonPoll.ino)

**Sketch:** [Physical Button State Sync](https://github.com/blynkkk/blynk-library/blob/master/examples/More/Sync/SyncPhysicalButton/SyncPhysicalButton.ino)