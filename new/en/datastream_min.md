### Data Stream min value

```min``` field is used in order to avoid unexpected values within the data stream.
For every value that matches the data stream type and less than ```min``` - ```min``` will value be used.

For example, you set the ```min``` value as ```0``` for your ```Integer``` data stream and 
hardware sends  ```-1```. In that case ```0``` value will be used instead of ```-1```.
The same rule applies for HTTPS API and any user input on the web or mobile application.