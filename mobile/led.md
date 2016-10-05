
### LED

A simple LED for indication. You need to send 0 in order to turn LED off. And 255 in order to turn LED on. Or just use
Blynk API as described below :

```cpp
WidgetLED led1(V1); //register to virtual pin 1
led1.off();
led1.on();
```
    
All values between 0 and 255 will change LED brightness :

```cpp
WidgetLED led2(V2);
led2.setValue(127); //set brightness of LED to 50%.
```

You can also change LED color with : 

```
Blynk.virtualWrite(V1, "color", "#D3435C"); //#D3435C - Blynk RED 
```

**Sketch:** [LED](https://github.com/blynkkk/blynk-library/blob/master/examples/Widgets/LED/LED_Blink/LED_Blink.ino)