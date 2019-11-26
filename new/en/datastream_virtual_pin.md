### Datastream: Virtual Pin

Virtual Pin is a way to exchange data between hardware, web, and mobile apps. 
Think about Virtual Pins as a variable where you can store and retrieve data from sensors, actuators, etc.

For example, you can read a value in Celsius from a temperature sensor like DHT11 (using a physical pin on your hardware), 
then convert this temperature to Fahrenheit and save the processed value to a Virtual Pin 01.

```cpp

void temperatureSend()                          // a function that is called by some timer
{
   temperatureCelsius = analogRead(A0);         // Reading sensor data in Celsius
   toFarenheit = temperatureCelsius*1.8 + 32;   // Converting Celsius to Farenheit
   
   Blynk.virtualWrite(V0, toFarenheit);         // Writing temperature in Farenheit to Virtual Pin V0
                                                // Now it can be used by widgets in the apps
}
```

Or you can send a command from the app to a Virtual Pin, and run a function inside a Virtual Pin handler.

```cpp

BLYNK_WRITE(V1)                                 // Device is waiting for incoming value on Virtual Pin V1. 
{
   pinValue = param.asInt();                    // creating a variable that will store incoming value
   
   if (pinValue == 1)                           // checking if incoming value is 1
   {
      doThis();                                 // trigger some function in your code
      doThat();                                 // trigger another function in your code
   }
}
```

Check examples in different languages on how to read and write data to Virtual Pins.
