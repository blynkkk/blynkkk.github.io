# Datastream: Data Type

Every Datastream has a Data Type setting. Data Type is used to specify the type and format of the data and optimize data storage and further calculations.

Make sure you choose a correct Data Type for your data. Currently, these Data Types are supported:

| Type | Min | Max |
| :---: | :---: | :---: |
| `Integer` | -2,147,483,648 | 2,147,483,647 |
| `Double` | -1.8 x 10^300 | 4.9 x 10^-324 |
| `String` | any value is accepted |  |

**IMPORTANT:**

Blynk server will ignore values that don't match the Data Type

Example: if Datastream has Data Type set to `Integer`, but Hardware sends `123.45`, this value will be skipped because it is `Double`, not `Integer`.

If the incoming value goes out of range of Min or Max setting, this value will be "cropped" to match this setting.

