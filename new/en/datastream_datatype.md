### Datastream: Data Type

Every datastream has a Data Type setting. Data Type is used to specify the type and format of the data, and optimize data storage and further calculations.

Currently 3 Data Types are supported. Check guide below to make sure you choose a correct Data Type for your data. 

|      Type      |             Min             |              Max             |
|:--------------:|:---------------------------:|:----------------------------:|
| ```Integer```  |       -2,147,483,648        |         2,147,483,647        |
|   ```Float```  | 1.7976931348623157 x 10^308 | 4.9406564584124654 x 10^-324 |
|  ```String```  | any value is accepted                                      |


**IMPORTANT:**

Values that doesn't match the Data Type will be ignored by server.

Example: if Datastream has Data Type set to ```Integer```, but Hardware sends ```123.45```, this value will be skipped because it is ```Float```, not ```Integer```.

If incoming value goes out of range of Min or Max setting, this value will be "cropped" to match this setting. Read more here(link to min/max setting).
