### Datastream: Min/Max values

```Min / Max``` fields are used to specify the range of incoming values.
This setting is applied everywhere where this datastream is used. For example, if you use Chart widget, it will use min/max values by default. Some vizualization widgets allow overriding min/max setting.

**IMPORTANT:** If incoming value falls out of the specified min/max range, the value will be *cropped*. 

For example: Datastream `MIN-MAX` is set to `0-100`

| Datastream | Min | Max |
|----------------|--------|--------|
| Humidity             | `0`     | `100`|

Here is how incoming values will be processed:

| Incoming value | Result |
|----------------|--------|
| `50`             | `50`     |
| `314`            | `100`    |
|`-2`             | `0`      |


Min /Max settging will only be applied for values that matches the Data Type. Otherwise, the value will be ignored. Check Data Type Settings reference (link)
