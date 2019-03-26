
### Segmented Switch

Segmented Switch widget allows you to send command to your hardware based on selection you made on UI. Segmented Switch
sends index of element you selected and not label string. Sending index starts from 1.
It works same way as usual ComboBox or Menu element. 

Example code:
```cpp
BLYNK_WRITE {
  switch (param.asInt()) {
    case 1: { // Item 1
      Serial.println("Item 1 selected");
      break;
    }
    case 2: { // Item 2
      Serial.println("Item 2 selected");
      break;
    }    
  }
}
```

You can also set Menu items from hardware side with : 
```cpp
Blynk.setProperty(V1, "labels", "label 1", "label 2", "label 3");
```

**Sketch:** [Menu](https://github.com/blynkkk/blynk-library/blob/master/examples/Widgets/Menu/Menu.ino)