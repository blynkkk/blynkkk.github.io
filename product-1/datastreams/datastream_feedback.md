# Wait for confirmation from the device

In some cases, it's important to get a confirmation that hardware has received the command or value and use in the mobile app UI, for example.

This ****setting sets an interval of how long the mobile or web app will wait for the confirmation from the hardware.

## **Usage Example**

Imagine you have a garage door opener device and a mobile app that controls it. Let's say you need to disable the OPEN/CLOSE button in the mobile app 

1. You set Datastream for `garage_ door_status` to wait for confirmation from device to 5 sec. 
2. End-user pressed the button in the mobile app that should close the garage door.
3. If hardware confirms that command was processed and applied - the switch in the app will remain in ON state. ****
4. If there is no confirmation from the device that the door was closed within 5 seconds, the switch will go back to the initial OFF state.

Here is a code example that shows how you can make it work:

```cpp
BLYNK_WRITE(V1) // reading the button in the app
{   
  int value = param.asInt();  // processing incoming button value as integer
  
  // checking if button in tha app was pressed
  if (value == 1) { 
  // somewhere in the code, hardware confirms that door was actually opened     
     if (doorOpened()) {
       // enable the button in the app
       Blynk.setProperty(V1, "isDisabled", false)
     } else {
       // disable the button in the app
       Blynk.setProperty(V1, "isDisabled", true)
     }
  }
}
```

