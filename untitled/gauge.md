# Gauge

A great visual way to display incoming numeric values.

Can work in 2 modes :

* PUSH mode \(select if from Frequency Reading picker\);
* Frequency Reading mode;

In PUSH mode you update gauge from hardware side with code :

```cpp
Blynk.virtualWrite(V1, val);
```

In this mode every message that hardware sends to server is stored automatically on server. PUSH mode doesn't require application to be online or opened.

With Frequency Reading mode you need to select update interval and application will trigger events with required timing. Your application should be open and running in order to make requests to hardware. You don't need any code for Analog and Digital pins in that case. However for virtual pins you need to use next code :

```cpp
//triggered from app
BLYNK_READ(V1)
{
  //send to app
  Blynk.virtualWrite(V1, val);
}
```

## Formatting options

Gauge also has "Label" field which allows use to use formatting. Let's assume, your sensor sends number 12.6789 to Blynk application. Next formatting options are supported:

`/pin/` - displays the value without formatting \(12.6789\)

`/pin./` - displays the value without decimal part \(13\)

`/pin.#/` - displays the value with 1 decimal digit \(12.7\)

`/pin.##/` - displays the value with two decimal places \(12.68\)

## Other options

You can also change gauge label from hardware with :

```cpp
Blynk.setProperty(V1, "label", "My Gauge Label");
```

or change color :

```cpp
//#D3435C - Blynk RED
Blynk.setProperty(V1, "color", "#D3435C");
```

**Sketch:** [BlynkBlink](https://github.com/blynkkk/blynk-library/blob/master/examples/GettingStarted/BlynkBlink/BlynkBlink.ino)

