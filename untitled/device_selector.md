# Device Selector

Device selector is a powerful widget which allows you to update widgets based on one active device. This widget is particularly helpful when you have a fleet of devices with similar functionality.

Imagine you have 4 devices and every device has a Temperature & Humidity sensor connected to it. To display the data for all 4 devices you would need to add 8 widgets.

With Device Selector, you can use only 2 Widgets which will display Temperature and Humidity based on the active device chosen in Device Selector.

All you have to do is:

1. Add Device Selector Widget to the project
2. Add 2 widgets \(for example Value Display Widget\) to show Temperature and Humidity
3. In Widgets Settings you will be able assign them to Device Selector \(Source or Target section\)
4. Exit settings, Run the project. 

Now you can change the active device in Device Selector and you will see that Temperature and Humidity values are reflecting the data updates for the device you just picked.

**NOTE :**  Webhook Widget will not work with Device Selector \(yet\).

