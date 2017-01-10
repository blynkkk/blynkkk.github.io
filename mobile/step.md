
### Step Control

Step control is like 2 buttons assigned to 1 pin. One button increments your value by desired step and another 
one decrements it. It is very useful for use cases where you need to increment your values very precisely and you can't 
achieve this precision with slider widget.

You can change step state from hardware side. For example : 

```cpp
Blynk.virtualWrite(V1, val);
```

You can change step labels from hardware with : 

```cpp
Blynk.setProperty(V1, "label", "My Stepper");
```

or change color : 

```cpp
//#D3435C - Blynk RED 
Blynk.setProperty(V1, "color", "#D3435C");
```

You can also get step control state from server in case your hardware was disconnected with Blynk Sync feature : 

```cpp
BLYNK_CONNECTED() {
  Blynk.syncVirtual(V1);
}

BLYNK_WRITE(V1) {
  int stepperValue = param.asInt();
}
```

#### Home Screen Button

You can also add button to your Android Home Screen. Button works via HTTPS in that case. Have in mind that in "Home Screen" 
mode button has few limitations. It may not work instantly due to Android Widget limitations. Button will update it's 
state only once per 15 min. 

**Note :** Adding home screen widget costs 100 energy. This energy not rechargeable.


**Sketch:** [Basic Sketch](https://github.com/blynkkk/blynk-library/blob/master/examples/GettingStarted/BlynkBlink/BlynkBlink.ino)