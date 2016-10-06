
### Gauge

A great visual way to display incoming numeric values.

You can change gauge label from hardware with : 

```cpp
Blynk.virtualWrite(V1, "label", "My Gauge Label");
```

or change color : 

```cpp
Blynk.virtualWrite(V1, "color", "#D3435C"); //#D3435C - Blynk RED
```

**Sketch:** [BlynkBlink](https://github.com/blynkkk/blynk-library/blob/master/examples/GettingStarted/BlynkBlink/BlynkBlink.ino)