### Data Stream max value

```max``` field is used in order to avoid unexpected values within the data stream.
For every value that matches the data stream type and larger than ```max``` - ```max``` will value be used.

For example, you set the ```max``` value as ```10``` for your ```Integer``` data stream and 
hardware sends  ```11```. In that case ```10``` value will be used instead of ```11```.
The same rule applies for HTTPS API and any user input on the web or mobile application.