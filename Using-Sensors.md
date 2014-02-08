NOTE: This documentation applies to code that has not been released.

## Overview

One of the goals of ev3dev is to support as many sensors as possible. If you have a sensor that does not work, let us know about it.

When dealing with sensors in ev3dev, it is useful to know how it communicates with the EV3. This determines what you need to do to read data from your sensor.

### Analog Sensors

These are the simplest type of sensor. The measured value is converted to a voltage that is read by the EV3. There are actually two types of analog sensors. We call the first **Analog/EV3**. These are sensors that were designed specifically for the EV3 and will not work on the NXT. They contain an ID resistor so that the EV3 can tell different types of sensors apart. The second type is **Analog/NXT**. These sensors are designed for the NXT, but also work on the EV3. The EV3 cannot differentiate between these sensors though, so you have to tell it which one your have or just use a generic interface.

RCX sensors also fall into this category, but do not work with the EV3 - at least not with the converter cable described in the NXT Hardware Developers kit. This is due to a difference in the input port pins between the EV3 and the NXT. If someone wants to research the [LEGO 8528](http://shop.lego.com/en-US/Converter-Cables-for-LEGO-MINDSTORMS-NXT-8528/?domainredir=www.shop.lego.com) cable or design a new converter cable, we could probably make them work.

### I2C Sensors

I2C sensors are sensors that communicate with the intelligent brick via the [I2C communication protocol](https://en.wikipedia.org/wiki/I2c). In the NXT documentation, they are referred to a "digital" sensors.

These sensors can be sorted into two categories as well: those that were designed using LEGO's guidelines and those that use an off the shelf I2C chip. ev3dev supports both kind of sensors, but only the first type is auto-detected. We will refer to the former as **I2C/M** (for Mindstorms) and the latter as **I2C/S** (for Standard).

### UART Sensors

These are a new type of sensor designed for the EV3 (they don't work with the NXT). They use an [UART](https://en.wikipedia.org/wiki/Uart) to send data to the brick. These sensors are a bit "smarter" in that in addition to sending the data of what they measure, they also send information about their capabilities. This means that any new UART sensors should "just work" without us having to write new drivers.

## Usage

### The Mindstorms Sensor class

Most sensors are accessed using a device driver class especially for Mindstorms sensors. When you plug a sensor in (assuming it is the auto-detectable type) a sysfs node will be added to ```/sys/class/msensor```.

TODO: copy and modify stuff from [[Using UART Sensors]]

### I2C Sensor Considerations

I2C/M sensors should be auto-detected (check the table below for the status of individual sensors). They will show up in ```/sys/class/msensors``` and have the same interface as other sensors. They also have a couple extra attributes.

- ```vendor_id```
- ```product_id```
- ```firmware_ver```
- ```poll_ms```

I2C/S sensors are not autodetected because, well, there are just too many of them. But they are easy to load manually and you can write udev rules to load them automatically if you want. Most of these types of sensors do not use ```/sys/class/msensors``` because there are already existing drivers in the Linux kernel for many standard I2C chips. See the table below for the driver to use for each sensor.

## List of Sensors

