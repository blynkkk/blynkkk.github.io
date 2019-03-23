
### Labeled Value

Displays incoming data from your sensors or Virtual Pins. It is a better version of 'Value Display' as it has a formatting 
string, so you could format incoming value to any string you want.

Can work in 2 modes : 

- PUSH mode (select if from Frequency Reading picker);
- Frequency Reading mode;

In PUSH mode you update value display from hardware side with code : 
 
```cpp
Blynk.virtualWrite(V1, val); 
```

In this mode every message that hardware sends to server is stored automatically on server. PUSH mode doesn't require 
application to be online or opened.

With Frequency Reading mode you need to select update interval and application will trigger events with required timing. 
Your application should be open and running in order to make requests to hardware. You don't need any code for Analog and 
digital pins in that case. However for virtual pins you need to use next code : 

```cpp
//triggered from app
BLYNK_READ(V1)
{
  //send to app
  Blynk.virtualWrite(V1, val);
}
```

#### Formatting options

Let's assume, your sensor sends number 12.6789 to Blynk application.
Next formatting options are supported:

```/pin/``` - displays the value without formatting (12.6789)

```/pin./``` - displays the value without decimal part (13)

```/pin.#/``` - displays the value with 1 decimal digit (12.7)

```/pin.##/``` - displays the value with two decimal places (12.68)

#### Home Screen Labeled Value

You can also add Labeled Value to your Android Home Screen. Labeled Value works via HTTPS in that case. 
Have in mind that in "Home Screen" mode Labeled Value has few limitations. Labeled Value will update it's state only 
once per 15 min. You can change this via Widget Settings. However update interval less than 15 minutes is not guaranteed. 
You can also resize Labeled Value on Home Screen - just do long click on widget and resize it as you need.

**Note :** Adding home screen widget costs 100 energy. This energy not rechargeable.
**Note :** Home Screen Widgets for Local Blynk servers requires port 8080 to be opened.

**Sketch:** [BlynkBlink](https://github.com/blynkkk/blynk-library/blob/master/examples/GettingStarted/BlynkBlink/BlynkBlink.ino)