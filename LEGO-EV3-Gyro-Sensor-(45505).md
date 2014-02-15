IMPORTANT: This data has not been verified (because @dlech doesn't have one of these sensors!).

### General

This sensor uses the [[msensor|Using the Mindstorms Sensor Device Class]] device class.

|              | Value |
|:------------:|:-----:|
|```type_id``` | ```32```
| # Modes      | 5

### Modes

|   | Mode 0 | Mode 1 | Mode 2 | Mode 3 | Mode 4 |
|---|--------|--------|--------|--------|--------|
| ```mode``` | ```GYRO-ANG``` | ```GYRO-RATE``` | ```GYRO-FAS``` | ```GYRO-G&A``` | ```GYRO-CAL``` |
| Description | Angle | Rotational Speed | ??? | Angle and Rotational Speed | Calibration??? |
| ```num_values``` | ```1``` | ```1``` | ```1``` | ```2``` | ```4```
| ```value0``` | Angle | Rotational Speed | ??? | Angle | |
| &emsp;Min | | ```-180``` | ```-440```  | ```-2000```??? | ```-180``` | |
| &emsp;Max | | ```180``` | ```440``` | ```2000```??? | ```180``` | |
| ```value1``` | | | | Rotational Speed | |
| &emsp;Min | | | | | ```-440``` | |
| &emsp;Max | | | | | ```440``` | |
| ```units``` | ```deg``` (degrees) | ```d/s``` (degrees/second) | _none_ | _none_ | _none_
| ```dp``` (decimal places) | ```0``` | ```0``` | ```0``` | ```0``` | ```0```
Values in the tables that look like ```this``` are the names of sysfs attributes or values returned by said attributes.