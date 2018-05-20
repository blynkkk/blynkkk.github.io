
### Styled Button

Works in push or switch modes. Allows to send any number value on button click and button release events. By default  
button uses 0/1 (LOW/HIGH) values. Button sends 1 (HIGH) on press and sends 0 (LOW) on release.

You can change button state from hardware side. For example, turn on button assigned to virtual pin V1 : 

```cpp
Blynk.virtualWrite(V1, HIGH);
```

You can change button labels from hardware with : 

```cpp
Blynk.setProperty(V1, "onLabel", "ON");

Blynk.setProperty(V1, "offLabel", "OFF");
```

or change color of the button :

```cpp
Blynk.setProperty(V1, "onColor", "#D3435C");

Blynk.setProperty(V1, "offColor", "#D3435C");
```

or change background color of the button :

```cpp
Blynk.setProperty(V1, "onBackColor", "#D3435C");

Blynk.setProperty(V1, "offBackColor", "#D3435C");
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

**Sketch:** [Basic Sketch](https://github.com/blynkkk/blynk-library/blob/master/examples/GettingStarted/BlynkBlink/BlynkBlink.ino)

**Sketch:** [Physical Button Interrupt](https://github.com/blynkkk/blynk-library/blob/master/examples/More/Sync/ButtonInterrupt/ButtonInterrupt.ino)

**Sketch:** [Physical Button Poll](https://github.com/blynkkk/blynk-library/blob/master/examples/More/Sync/ButtonPoll/ButtonPoll.ino)

**Sketch:** [Physical Button State Sync](https://github.com/blynkkk/blynk-library/blob/master/examples/More/Sync/SyncPhysicalButton/SyncPhysicalButton.ino)