
### Labeled Value

Displays incoming data from your sensors or Virtual Pins. It is a better version of 'Value Display' as it has a formatting 
string, so you could format incoming value to any string you want.

#### Formatting options

Let's assume, your sensor sends number 12.6789 to Blynk application.
Next formatting options are supported:

```/pin/``` - displays the value without formatting (12.6789)

```/pin./``` - displays the value without decimal part (13)

```/pin.#/``` - displays the value with 1 decimal digit (12.7)

```/pin.##/``` - displays the value with two decimal places (12.68)

**Sketch:** [BlynkBlink](https://github.com/blynkkk/blynk-library/blob/master/examples/GettingStarted/BlynkBlink/BlynkBlink.ino)