### Offline Ignore Period

Offline ignore period is an option that allows you to hide "offline" event on the device timeline. For example, 
let's say you set the offline ignore period to 1 minute and we have the next device log:

17:44:33 - device connects
17:44:40 - device disconnects
17:44:50 - device connects again

With offline ignore period set to 1 minute your device timeline will show only 1 event:
 
17:44:33 device connects

This is because device reconnected within the 1 minute interval. 
Without offline ignore period set your timeline will show all the above events. 