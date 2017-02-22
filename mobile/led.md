
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

#### Home Screen LED

You can also add LED to your Android Home Screen. LED works via HTTPS in that case. Have in mind that in "Home Screen" 
mode LED has few limitations. LED will update it's state only once per 15 min. You can change this via Widget 
Settings. However update interval less than 15 minutes is not guaranteed. 

**Note :** Adding home screen widget costs 100 energy. This energy not rechargeable.
**Note :** Home Screen Widgets for Local Blynk servers requires port 8080 to be opened.

**Sketch:** [LED](https://github.com/blynkkk/blynk-library/blob/master/examples/Widgets/LED/LED_Blink/LED_Blink.ino)