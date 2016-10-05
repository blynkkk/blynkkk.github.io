
### zeRGBa

zeRGBa is usual RGB controller (color picker).

####Settings:

- **SPLIT**:
Each of the parameters is sent directly to the Pin on your hardware (e.g D7). You don't need to write any code.

**NOTE:** In this mode you send multiple commands from one widget, which can reduce performance of your hardware.

Example: If you have a zeRGBa Widget and it's set to D1, D2, D3 it will send 3 commands over the Internet:

```cpp
digitalWrite(1, value);
digitalWrite(2, value);
digitalWrite(3, value);
```

- **MERGE**:
When MERGE mode is selected, you are sending just 1 message, consisting of array of values. But you'll need to parse it on the hardware. 

This mode can be used with Virtual Pins only.
	
Example: Add a zeRGBa Widget and set it to MERGE mode. Choose Virtual Pin V1.
	
```cpp
BLYNK_WRITE(V1) // There is a Widget that WRITEs data to V1 
{
    int r = param[0].asInt(); // get a RED channel value
	int g = param[1].asInt(); // get a GREEN channel value
	int b = param[2].asInt(); // get a BLUE channel value
}
```
 
- Send On Release:
**Send On Release** is available for most controller widgets and allows you to decrease data traffic on your hardware. 
For example, when you move joystick widget, commands are continuously streamed to the hardware, during a single joystick move 
you can send dozens of commands. There are use-cases where it's needed, however creating such a load may cause hardware reset. 
We recommend enabling **Send On Release** feature for most of the cases, unless you really need instant feedback.
This option is enabled by default.
