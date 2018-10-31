
### Image

Image widget allows you to display any image within your project. You need to provide http/s url to it.
Url should be valid endpoint to the binary data of the image.

Right now image widget supports 2 display options:
 - **Fit**: Image will be scaled to fit height or width of the widget size;
 - **Fill**: Image will be scaled to fill widget area. Cropping may occur;

You can make image widget interactive by providing multiple links to different images
with different states and change displayed image index from your hardware or via Eventor widget.

For example, select the first icon from the list :

```cpp
Blynk.virtualWrite(V1, 1); //image indexing starts from 1
```

You can also change opacity, scale or rotation of the displayed the image :

```cpp
Blynk.setProperty(V1, "opacity", 50); // 0-100%
```

```cpp
Blynk.setProperty(V1, "scale", 30); // 0-100%
```

```cpp
Blynk.setProperty(V1, "rotation", 10); //0-360 degrees
```

also, you can fully replace the list of image from the hardware:

```cpp
Blynk.setProperty(V1, "urls", "https://image1.jpg", "https://image2.jpg");
```

or you can change individual image by it index:

```cpp
Blynk.setProperty(V1, "url", 1, "https://image1.jpg");
```

