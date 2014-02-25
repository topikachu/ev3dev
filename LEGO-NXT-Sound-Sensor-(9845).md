### General

This sensor uses the [[msensor|Using the Mindstorms Sensor Device Class]] device class.

|              | Value      |
|:------------:|:----------:|
|```type_id``` | ```125```  |
| # Modes      | 2          |
| Connection   | Analog/NXT |

### Modes

<table>
  <tr>
    <th>
    <th>Mode 0
    <th>Mode 1
  <tr>
    <td><code>mode</code>
    <td><code>NXT-ANALOG-0</code>
    <td><code>NXT-ANALOG-1</code>
  <tr>
    <td>Description
    <td>Sound Intensity - Flat
    <td>Sound Intensity - A-weighting
  <tr>
    <td><code>num_values</code>
    <td><code>1</code>
    <td><code>1</code>
  <tr>
    <td><code>value0</code>
    <td>Intensity
    <td>Intensity
  <tr>
    <td>&emsp;Min
    <td><code>0</code> (default scaling)
    <td><code>0</code> (default scaling)
  <tr>
    <td>&emsp;Max
    <td><code>5000</code> (default scaling)
    <td><code>5000</code> (default scaling)
  <tr>
    <td><code>units</code>
    <td><i>none</i>
    <td><i>none</i>
  <tr>
    <td><code>dp</code> (decimal places)
    <td><code>0</code>
    <td><code>0</code>
</table>
Values in the tables that look like ```this``` are the names of sysfs attributes or values returned by said attributes.
