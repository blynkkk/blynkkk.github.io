### Data Stream value confirmation

For some critical actions it is very important to know that hardware actually received the command 
and applied the received value from the user input.

For such use cases Data Stream has confirmation property. It allows you to setup the interval 
during which user can wait for the response from the device, 
while the widget used to send the value will be disabled.

For example, let's assume you have a garage door and which you can open by sending the ```1``` value 
via the button that is assigned to the Virtual Data Stream on ```V1``` and 
you have set the ```Wait for confirmation``` period for 5 seconds. 

When you click on the button - it sends ```1``` value to the hardware. 
In case hardware is online and accepts the value - it can send back the applied value 
(telling us that door was successfully opened). If hardware wasn't online or haven't 
send any confirmation sue to error or non acceptable value - 
data stream value will be reverted to the previous value. 

Here is a simplest code example that shows how you can make it work:

```
BLYNK_WRITE(V1)
{   
  int value = param.asInt();
  if (value == 1) {
     if (openDoor()) {
       Blynk.virtualWrite(V1, "1"); // confirm the value, ui will enable the button
     } else {
       Blynk.virtualWrite(V1, "0"); // you can send back any other value, 
                                    // saying that change was unsuccessful
                                    // ui will enable the button
     }
  }
}
```