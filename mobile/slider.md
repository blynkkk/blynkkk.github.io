
### Slider

Similar to potentiometer. Allows to send values between MIN and MAX.
 
You can change slider state from hardware side. For example, set slider value assigned to virtual pin V1 to 55 : 

```cpp
Blynk.virtualWrite(V1, 55);
```

You can change slider label from hardware with : 

```cpp
Blynk.setProperty(V1, "label", "My Slider Label");
```

or change color : 

```cpp
//#D3435C - Blynk RED
Blynk.setProperty(V1, "color", "#D3435C");
```
 
### Send On Release
**Send On Release** is available for most controller widgets and allows you to decrease data traffic on your hardware. 
For example, when you move slider widget, commands are continuously streamed to the hardware, during a single slider move 
you can send dozens of commands. There are use-cases where it's needed, however creating such a load may cause hardware reset. 
We recommend enabling **Send On Release** feature for most of the cases, unless you really need instant feedback.
This option is enabled by default.

**Sketch:** [Basic Sketch](https://github.com/blynkkk/blynk-library/blob/master/examples/GettingStarted/BlynkBlink/BlynkBlink.ino)