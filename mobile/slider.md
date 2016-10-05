
### Slider

Similar to potentiometer. Allows to send values between MIN and MAX.
 
### Send On Release
**Send On Release** is available for most controller widgets and allows you to decrease data traffic on your hardware. 
For example, when you move slider widget, commands are continuously streamed to the hardware, during a single slider move 
you can send dozens of commands. There are use-cases where it's needed, however creating such a load may cause hardware reset. 
We recommend enabling **Send On Release** feature for most of the cases, unless you really need instant feedback.

**Sketch:** [BlynkBlink](https://github.com/blynkkk/blynk-library/blob/master/examples/GettingStarted/BlynkBlink/BlynkBlink.ino)