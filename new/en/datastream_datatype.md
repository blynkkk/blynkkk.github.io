### Data Stream: Data Type

Every data stream has a data type. Data type is used to optimize the data storage and calculations.

Currently there are 3 supported data types. Check guide below to make sure you choose a correct Data Type for your data. 

- ```Integer``` (-2,147,483,648 to 2,147,483,647)
- ```Float``` (1.7976931348623157 x 10^308 to 4.9406564584124654 x 10^-324)
- ```String``` (any value is accepted)

**IMPORTANT:**

Values that doesn't match the Data Type will be ignored by server.

Example: if Datastream has Data Type set to ```Integer```, but Hardware sends ```123.45```, this value will be skipped because it is ```Float```, not ```Integer```.

If incoming value goes out of range of Min or Max setting, this value will be "cropped" to match this setting. Read more here(link to min/max setting).
