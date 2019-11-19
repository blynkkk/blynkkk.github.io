### Data Stream sync

Marking Data Stream as ```sync``` - allows you to get the Data Stream value from that Data Stream via 
```Blynk.sync()``` or ```Blynk.syncAll()``` api.

```cpp
BLYNK_CONNECTED() {
  // request the values for all data streams
  // that marked as sync data streams
  Blynk.syncAll();
}
```

In the example above server will return the values only for Data Streams that were marked as ```sync```.

This was done in done in order to minimize the traffic between server and hardware so you can sure 
that only requested stream values are sent back.