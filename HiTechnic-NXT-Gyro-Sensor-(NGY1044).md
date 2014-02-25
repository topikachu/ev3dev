### General

This sensor uses the [[msensor|Using the Mindstorms Sensor Device Class]] device class.

|              | Value      |
|:------------:|:----------:|
|```type_id``` | _N/A_      |
| # Modes      | 1          |
| Connection   | Analog/NXT |

### Modes

<table>
  <tr>
    <th>
    <th>Mode 0
  <tr>
    <td><code>mode</code>
    <td><code>NXT-ANALOG-0</code>
  <tr>
    <td>Description
    <td>Rotational speed
  <tr>
    <td><code>num_values</code>
    <td><code>1</code>
  <tr>
    <td><code>value0</code>
    <td>Rotational speed
  <tr>
    <td>&emsp;Min
    <td><code>0</code> (default scaling)
  <tr>
    <td>&emsp;Max
    <td><code>4883</code> (default scaling)
  <tr>
    <td><code>units</code>
    <td><i>none</i>
  <tr>
    <td><code>dp</code> (decimal places)
    <td><code>0</code>
</table>
Values in the tables that look like ```this``` are the names of sysfs attributes or values returned by said attributes.

### Scaling

Since this is an NXT Analog sensor and the exact type cannot be autodetected, we have to use a generic sensor interface. This sensor measures rotational speed in degrees/second. Nominally, 0.00V == -540 deg/sec and 4.88V == 400 deg/sec. However, depending on temperature, there is a small offset, so we have to calibrate the sensor to accommodate this.

Sample calibration code:

```bash
#!/bin/bash

# sample the raw sensor voltage 10 times and get an average value
total=0
for i in {1..10}
do
        total=$(($total + $(od -A n -N 4 -t d4 bin_data)))
done
average=$(($total / $i))

# Set scaling that includes offset from average
# 1.953V is proportional to 400 deg/sec
echo $average > raw_min
echo $(($average + 1953)) > raw_max
echo 0 > scaled_min
echo 400 > scaled_max
```