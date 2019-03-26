
### Push Notifications

Push Notification widget allows you to send push notification from your hardware to your device. Currently it also 
contains 2 additional options :

- **Notify when hardware offline** - you will get push notification in case your hardware went offline.
- **Offline Ignore Period** - defines how long hardware could be offline (after it went offline) before sending notification. 
In case period is exceeded - "hardware offline" notification will be send. You will get no notification in case hardware 
was reconnected within specified period.
- **Priority** high priority gives more chances that your message will be delivered without any delays. 
See detailed explanation [here](https://developers.google.com/cloud-messaging/concept-options#setting-the-priority-of-a-message). 

**WARNING** : high priority contributes more to battery drain compared to normal priority messages.

Example code:
```cpp
Blynk.notify("Hey, Blynkers! My hardware can push now!");
```

You can also use placeholder for device name, that will be replaced on the server with your device name:
```cpp
Blynk.notify("Hey, Blynkers! My {DEVICE_NAME} can push now!");
```


Limitations :

- Maximum allowed body length is 120 symbols;
- Every device can send only 1 notification every 5 seconds;

### Unicode in push notifications

The library handles all strings as UTF8 Unicode. If you're facing problems, try to print your message to the Serial 
and see if it works (the terminal should be set to UTF-8 encoding). If it doesn't work, probably you should read 
about unicode support of your compiler. 
If it works, but your message is truncated - you need to increase message length limit 
(all Unicode symbols consume at least twice the size of Latin symbols).

### Increasing message length limit

You can increase maximum message length by putting on the top of your sketch (before Blynk includes):
```cpp
#define BLYNK_MAX_SENDBYTES 256 // Default is 128
```

**Sketch:** [PushNotification](https://github.com/blynkkk/blynk-library/blob/master/examples/Widgets/PushNotification/PushNotification_Button/PushNotification_Button.ino)
