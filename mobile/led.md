
### LED

A simple LED for indication. You need to send 0 in order to turn LED off. And 255 in order to turn LED on. Or just use
Blynk API as described below :

```cpp
//register to virtual pin 1
WidgetLED led1(V1);
led1.off();
led1.on();
```
    
All values between 0 and 255 will change LED brightness :

```cpp
WidgetLED led2(V2);
//set brightness of LED to 50%.
led2.setValue(127); 
```

You can also change LED color with : 

```cpp
//#D3435C - Blynk RED 
Blynk.setProperty(V1, "color", "#D3435C"); 
```

**Sketch:** [LED](https://github.com/blynkkk/blynk-library/blob/master/examples/Widgets/LED/LED_Blink/LED_Blink.ino)