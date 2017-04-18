
### Map

Map widget allows you set points/pins on map from hardware side. This is very useful widget in case you have 
multiple devices and you want track their values on map.

You can send a point to map with regular virtual write command :  

```cpp
Blynk.virtualWrite(V1, pointIndex, lat, lon, "value");
```

We also created a wrapper for you to make usage of map simpler : 

You can change button labels from hardware with : 

```cpp
WidgetMap myMap(V1);
...
int index = 1;
float lat = 51.5074;
float lon = 0.1278;
myMap.location(index, lat, lon, "value");
```

Using save ```index``` allows you to override existing point value.

**Sketch:** [Basic Sketch](https://github.com/blynkkk/blynk-library/blob/master/examples/Widgets/Map/Map.ino)