
### Twitter

Twitter widget connects your Twitter account to Blynk and allows you to send Tweets from your hardware.

Example code:
```cpp
Blynk.tweet("Hey, Blynkers! My Arduino can tweet now!");
```

Limitations :

- you can't send 2 tweets with same message (it's Twitter policy)
- only 1 tweet per 15 seconds is allowed

### Unicode in Twitter

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

**Sketch:** [Twitter](https://github.com/blynkkk/blynk-library/blob/master/examples/Widgets/Twitter/Twitter.ino)