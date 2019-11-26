### Events: Notification Period

Notification Period defines how often notifications are sent for this particular event.

For example, a 1 minute period means end-users won't get more than one notification per 1 minute, 
even if hardware or API sends more. After 1 minute since the last posted notification expires, 
new notifications will get in.

Notification Period is applied per event per device. 
If you have two events with different notification periods set up within the same device, 
they will be processed independently and end-users will get both notifications with different periods.
