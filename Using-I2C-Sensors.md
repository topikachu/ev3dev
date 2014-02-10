## Kinds of I2C Devices

The I2C standards only specify how data is sent from device to device. It does not specify the layout of the registers of a device. LEGO, however, has guidelines for 3rd party manufactures so that they can provide sensors with (fairly) uniform register layout.

We call sensors that were designed following LEGO's guidelines **I2C/M** sensors (M is for Mindstorms). This common register layout lets us autodetect the type of sensor and proved access to the sensor via the ```msensor``` class.

We refer to sensors that do not conform to LEGO's specifications as **I2C/S** sensors (S is for Standard). There are so many types of I2C chips in the wild that are already supported on Linux, that we do not attempt to autodetect them. To use them, we just need to find a compatible driver and manually load it.

## Addressing

The I2C address that is used in ev3dev is different from the other EV3/NXT programming languages/environments. See [[I2C Sensor Addressing]] to find out how and why. Since most sensors are autodetected, you don't usually have to worry about the address. However, for manually loading devices, you need to know what the address is. Also, if you had multiple sensors connected to a single port using a port splitter, you would need to know the address to make sure your are using the correct ```sensorN``` device node. NOTE: A [port splitter](http://mindsensors.com/index.php?module=pagemaster&PAGE_user_op=view_page&PAGE_id=79) is not the same as a [sensor MUX](http://mindsensors.com/index.php?module=pagemaster&PAGE_user_op=view_page&PAGE_id=179).

## Using I2C/M Sensors

See [[Using the Mindstorms Sensor Device Class]] for general usage. This is the I2C specific usage.

### Polling

By default, I2C/M sensors are polled every 100 milliseconds. This value can be changed via a module parameter. More on that later.

When we say "polled", we just mean that the EV3 brick initiates a read command to read data from the sensor. The data that is read depends on the current mode that is selected. You can change the polling rate using the ```poll_ms```. You can also disable polling by setting ```poll_ms``` to ```0```. When polling is disabled, you can initiate a data read by setting the mode again.

### Writing to the Sensor

We can write data to I2C sensors using the ```bin_data``` attribute. The first byte is the address of the register you want to write to and the following bytes are the data that is written to that register.

Example: Sending a "calibrate white" command to the mindsensor.com Light Sensor Array.

```bash
$ echo -e -n "\x41W" > bin_data
```
This writes the ascii character 'W' to register 0x41

### The ```nxt-i2c-sensor``` Module

All of the I2C/M drivers are part of the ```nxt-i2c-sensor``` module. It allows control over some of its behaviors via module parameters.

| Parameter        | Default | Description
|------------------|---------|------------
| allow_autodetect | Y       | Setting to ```N``` disables autodetection of sensors.
| default_poll_ms  | 100     | This provided the default value for the ```poll_ms``` attribute. A value of 0 will disable polling by default. Values of less that the minimum 50 msec will be rounded up to 50 msec. Changes only affect sensors plugged in after the change was made.

You can change the values at any time using ```/sys/module/nxt_i2c_sensor/parameters/*``` or you can make the changes permanent by adding a [.conf](http://manpages.debian.net/cgi-bin/man.cgi?query=modprobe.d&apropos=0&sektion=0&manpath=Debian+7.0+wheezy&format=html&locale=en) file to ```/etc/modprobe.d```.

### Manually Loading Devices

If you have autodetection disabled or if you have managed to changed the I2C address of your sensor to something other than the default, you will have to manually load a device in order to be able to use your sensor. We just have to tell the I2C adapter which driver to use and what address it is at. (You read the [addressing](./Using-I2C-Sensors#addressing) section didn't you?)

The I2C adapter device nodes are at ```/sys/bus/i2c/devices/i2c-N``` where N is the number of the input port plus 2. To load a device, we write to the ```new_device``` attribute.

```bash
$ echo nxt-i2c-sensor 0x15 > /sys/bus/i2c/devices/i2c-5/new_device
```

## Using I2C/S Sensors

As we already discussed, I2C/S sensors generally have an existing Linux driver that you can use. This means that each sensor will work a bit differently.



## Practical examples

### Changing the Polling Rate

Using the NXT Ultrasonic Sensor:

```bash
$ cat poll_ms
100
$ while true; do cat value0; done
22
23
26
27
30
25
...
22
24
26
26
22
22
^C
$ echo 1000 > poll_ms
$ while true; do cat value0; done
22
22
22
22
22
22
22
25
25
25
25
25
25
25
25
...
^C
$ echo 0 > poll_ms
$ cat value0 # value0 will be last value measured before polling stopped
23
$ cat value 0 # move the sensor and try again
23
$ cat mode
[NXT-US-CM] NXT-US-IN NXT-US-SI-CM NXT-US-SI-IN NXT-US-LIST
$ echo NXT-US-CM > mode # reads data
$ cat value0
29
$ cat value0 # move the sensor and try again
29
```
```^C``` means you have to press CTRL+C to make the loop stop.

### Sample ```/etc/modprobe.d/nxt-i2c-sensor.conf```

```bash
# Module configuration for nxt-i2c-sensor

# Uncomment this line to disable polling
#options nxt-i2c-sensor default_poll_ms=0

# Uncomment this line to disable autodetection
#options nxt-i2c-sensor allow_autodetect=N
```