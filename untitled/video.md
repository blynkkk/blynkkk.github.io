# Video Streaming

Simple widget that allows you to display any live or video stream. Widget supports RTSP \(RP, SDP\), HTTP/S progressive streaming, HTTP/S live streaming. For more info please follow [official Android documentation](https://developer.android.com/guide/appendix/media-formats.html).

At the moment Blynk doesn't provide streaming servers. So you can either stream directly from camera, use 3-d party services or host streaming server on own server \(on raspberry for example\).

You can also stop/start video stream with click on widget.

You can also change video url from hardware with :

```cpp
Blynk.setProperty(V1, "url", "http://my_new_video_url");
```

