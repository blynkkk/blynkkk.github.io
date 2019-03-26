
### Music Player

Simple UI element with 3 buttons - simulates music player interface. Every button sends it's own command to hardware : 
```play```, ```stop```, ```prev```, ```next```.

You can change widget state within the app from hardware side with next commands:

```
Blynk.virtualWrite(Vx, “play”);
Blynk.virtualWrite(Vx, “stop”);
```

You can also change widget play/stop state with next code (equivalent to above commands) : 

```Blynk.setProperty(V1, "isOnPlay", "false");```

**Sketch:** [Music Player](https://github.com/blynkkk/blynk-library/blob/master/examples/Widgets/Player/Player.ino)