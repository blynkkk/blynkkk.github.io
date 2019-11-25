### Datastream: Wait for confirmation from the device

In some cases, it's crucial to get a confirmation that hardware has received the command or value.

**Wait for confirmation from device** property allows you to set the interval for how long the mobile or web app will wait for the confirmation from the hardware.

Example: 
1. You set Datastream for garage door status to wait for confirmation for 5 sec. 
2. The user pressed the switch in the mobile app that should close the garage door.
3. If hardware confirms that command was processed and applied - the switch in the app will remain in ON state.
4. If there is no confirmation from the device that the door was closed within 5 seconds, the switch will go back to the initial OFF state.


Here is a code example that shows how you can make it work:

```cpp
BLYNK_WRITE(V1)
{   
  int value = param.asInt();
  if (value == 1) {
     if (openDoor()) {
       // confirm the value, UI will enable the button
       Blynk.virtualWrite(V1, "1");
     } else {
       // you can send back any other value, 
       // saying that change was unsuccessful
       // UI will enable the button
       Blynk.virtualWrite(V1, "0");
     }
  }
}
```
