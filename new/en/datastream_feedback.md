### Datastream: Wait for confirmation from device

In some cases it's important to know get a confirmation that hardware have received the command or value.

**Wait for confirmation from device** property allows you to set the interval for how long the mobile or web app will wait for the confirmation from hardware.

Example: 
1. You set Datastream for garage door status to wait for confirmation for 5 sec. 
2. User pressed the switch in the mobile app that should close the garage door.
3. If hardware confirms that command was processed and applied - the switch in the app will remail in ON state
4. If there is no confirmation from device that command the door was closed within 5 seconds, the switch will go back to initial OFF state


Here is a simplest code example that shows how you can make it work:

```
BLYNK_WRITE(V1)
{   
  int value = param.asInt();
  if (value == 1) {
     if (openDoor()) {
       // confirm the value, ui will enable the button
       Blynk.virtualWrite(V1, "1");
     } else {
       // you can send back any other value, 
       // saying that change was unsuccessful
       // ui will enable the button
       Blynk.virtualWrite(V1, "0");
     }
  }
}
```
