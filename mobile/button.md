
### Button

Works in push or switch modes. Allows to send any number value on button click and button release events. By default  
button uses 0/1 (LOW/HIGH) values. Button sends 1 (HIGH) on press and sends 0 (LOW) on release.

You can change button state from hardware side. For example, turn on button assigned to virtual pin V1 : 

```cpp
Blynk.virtualWrite(V1, HIGH);
```

You can change button labels from hardware with : 

```cpp
Blynk.setProperty(V1, "onLabel", "ON");
```

```cpp
Blynk.setProperty(V1, "offLabel", "OFF");
```

or change color : 

```cpp
//#D3435C - Blynk RED 
Blynk.setProperty(V1, "color", "#D3435C");
```

You can also get button state from server in case your hardware was disconnected with Blynk Sync feature : 

```cpp
BLYNK_CONNECTED() {
  Blynk.syncVirtual(V1);
}

BLYNK_WRITE(V1) {
  int buttonState = param.asInt();
}
```

#### Home Screen Button

You can also add button to your Android Home Screen. Button works via HTTPS in that case. Have in mind that in "Home Screen" 
mode button has few limitations. It may not work instantly due to Android Widget limitations. Button will update it's 
state only once per 15 min. 

**Note :** Adding home screen widget costs 100 energy. This energy not rechargeable.
**Note :** Home Screen Widgets not supported for Local Blynk servers.


**Sketch:** [Basic Sketch](https://github.com/blynkkk/blynk-library/blob/master/examples/GettingStarted/BlynkBlink/BlynkBlink.ino)

**Sketch:** [Physical Button Interrupt](https://github.com/blynkkk/blynk-library/blob/master/examples/More/Sync/ButtonInterrupt/ButtonInterrupt.ino)

**Sketch:** [Physical Button Poll](https://github.com/blynkkk/blynk-library/blob/master/examples/More/Sync/ButtonPoll/ButtonPoll.ino)

**Sketch:** [Physical Button State Sync](https://github.com/blynkkk/blynk-library/blob/master/examples/More/Sync/SyncPhysicalButton/SyncPhysicalButton.ino)