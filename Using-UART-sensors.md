@dlech has been working on UART sensor support. It is now ready for testing. Please see [mindboards/ev3dev-kernel issue #15](https://github.com/mindboards/ev3dev-kernel/pull/15) for the steps required to install the kernel and packages. Report any issues or suggestions there as well.

Known issues:
- Input port 1 is disabled. You will see this error in ```dmesg```:

    ```
    ev3-input-port: probe of in1 failed with error -22
    ```

- Sensors on ports 3 or 4 may reset themselves. ```dmesg``` will show:

    ```
    tty ttySU1: Reconnected due to: No data since last keep-alive.
    ```

    This is due to the PRU soft-UART not interrupting when it has received data in a timely manor. We may have to figure out how to build our own PRU frimware to fix this.

# Overview
When you plug in a UART sensor, it will appear in ```/sys/bus/legoev3/devices/``` as ```ttySX:ev3-uart-sensor```.

Here is a table to map input ports to ttys.
<table>
<tr><th>port<th>tty
<tr><td>1<td>ttyS1
<tr><td>2<td>ttyS0
<tr><td>3<td>ttySU1
<tr><td>4<td>ttySU0
</table>

I realize that it would be better to have the device name as ```inX:ev3-uart-sensor``` instead of ```ttySX...```, but I haven't figured out a good way to do it yet, so this is the way it is for now.

For an example, I will be using the EV3 Color Sensor in input port 2.

```sh
$ cd /sys/bus/legoev3/devices/ttyS0\:ev3-uart-sensor
$ ls
bin_data         modalias    pct_min  si_min     uevent  value3  value7
bin_data_format  mode        raw_max  si_units   value0  value4
device_type      num_values  raw_min  subsystem  value1  value5
dp               pct_max     si_max   type_id    value2  value6
```

Each sensor has a number of modes in which in can operate. You can view and change the modes using the ```mode``` attribute.

```sh
$ cat mode
[COL-REFLECT] COL-AMBIENT COL-COLOR REF-RAW RGB-RAW COL-CAL
$ echo COL-COLOR > mode
$ cat mode
COL-REFLECT COL-AMBIENT [COL-COLOR] REF-RAW RGB-RAW COL-CAL
```

Each mode has three pairs of min/max values that are received from the sensor. I am not sure why because only one applies per mode and from what I have seen, pct is always 0..100 and raw is always the same as si. So, I would suggest to only look at the si values.

```sh
$ cat raw_min
0
$ cat raw_max
8
$ cat pct_min
0
$ cat pct_max
100
$ cat si_min
0
$ cat si_max
8
```

The values measured by the sensor are read through the ```valueX``` attributes. The ```num_values``` attributes will tell you how many values there are. Values with an index >= num_values will return an error.

```sh
$ cat num_values
1
$ cat value*
0
cat: value1: No such device or address
cat: value2: No such device or address
cat: value3: No such device or address
cat: value4: No such device or address
cat: value5: No such device or address
cat: value6: No such device or address
cat: value7: No such device or address
$ echo RGB-RAW > mode
$ cat num_values
3
$ cat value*
4
6
2
cat: value3: No such device or address
cat: value4: No such device or address
cat: value5: No such device or address
cat: value6: No such device or address
cat: value7: No such device or address
```

## Advanced

Each type of UART sensor has a unique device id. You can see what it is with the ```type_id``` attribute.

```sh
$ cat type_id
29
```

The values use a fixed point decimal notation. The number of decimal places is returned by the ```dp``` attribute. The color sensor returns ```0``` in all modes, so I don't have a real-life example, but if ```dp``` was ```1``` and ```value0``` was ```123```, then the actual value would be ```12.3```.

```sh
$ cat dp
0
```

The ```bin_data``` attribute gives you access to the "raw" data from the sensor. The ```bin_data_format``` attribute tells you how to interpret the data.

<table>
<tr><th>bin_data_format<br>value<th>Meaning
<tr><td>s8<td>Signed 8-bit values (up to 32 values)
<tr><td>s16<td>Signed 16-bit values (up to 16 values)
<tr><td>s32<td>Signed 32-bit values (up to 8 values)
<tr><td>float<td>IEEE 754 32-bit floating point values (up to 8 values)
</table>

All values are little-endian, so no special conversion should be needed. If you try to read more than 32 bytes, you will get an error.

```sh
$ echo RGB-RAW > mode
$ cat bin_data_format
s16
$ hexdump < bin_data
0000000 0005 0006 0002 028f 0000 0000 0000 0000
0000010 0000 0000 0000 0000 0000 0000 0000 0000
0000020
$ echo COL-COLOR > mode
$ cat bin_data_format
s8
$ hexdump -e '8/1 "%02X " "\n"' -n $(cat num_values) < bin_data
07                     
```

You can also write data to the sensor, but I don't know of any need for this at the moment. When you run a program on the standard LEGO firmware, the byte 0x11 is written to each sensor when the program starts. I don't know what this accomplishes though. You can simulate this with the following command:

```sh
$ echo -e -n "\021" > bin_data
```

## Sensors
- [[EV3 Color Sensor|Using the EV3 Color Sensor]]
- [[EV3 Infrared Sensor|Using the EV3 Infrared Sensor]]
- [[EV3 Gyro Sensor|Using the EV3 Gyro Sensor]]
- [[EV3 Ultrasonic Sensor|Using the EV3 Ultrasonic Sensor]]