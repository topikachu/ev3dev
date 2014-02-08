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

<table>
  <tr>
    <th>Manufacturer
    <th>Mfg. P/N
    <th>Name
    <th>Connection Type
    <th>Autodetected
    <th>Driver Name
  <tr>
    <td rowspan="1"><a href="http://www.codatex.com//">CODATEX</a>
    <td>
    <td>Codatex RFID Sensor
    <td>
    <td>
    <td>
  <tr>
    <td rowspan="1"><a href="http://www.dexterindustries.com/">Dexter Industries</a>
    <td>
    <td>
    <td>
    <td>
    <td>
  <tr>
    <td rowspan="17"><a href="http://www.hitechnic.com/">HiTechnic</a>
    <td>NAA1030
    <td>NXT Angle Sensor
    <td>I2C/M
    <td>Y
    <td>[[ht-naa1030]]
  <tr>
    <td>NAC1040
    <td>NXT Acceleration / Tilt Sensor
    <td>I2C/M
    <td>Y
    <td>[[ht-nac1040]]
  <tr>
    <td>NBR1036
    <td>NXT Barometric Sensor
    <td>I2C/M
    <td>Y
    <td>[[ht-nbr1036]]
  <tr>
    <td>NCO1038
    <td>NXT Color Sensor V2
    <td>I2C/M
    <td>Y
    <td>[[ht-nco1038]]
  <tr>
    <td>NEO1048
    <td>NXT EOPD
    <td>Analog/NXT
    <td>Y*
    <td>
  <tr>
    <td>NFS1074
    <td>NXT Force Sensor
    <td>Analog/NXT
    <td>Y*
    <td>
  <tr>
    <td>NGY1044
    <td>NXT Gyro Sensor
    <td>Analog/NXT
    <td>Y*
    <td>
  <tr>
    <td>NIL1046
    <td>NXT IRLink Sensor
    <td>I2C/M
    <td>Y
    <td>[[ht-nil1046]]
  <tr>
    <td>NIS1070
    <td>NXT PIR Sensor
    <td>I2C/M
    <td>Y
    <td>[[ht-nis1070]]
  <tr>
    <td>NIR1032
    <td>NXT IRReceiver Sensor
    <td>I2C/M
    <td>Y
    <td>[[ht-nir1032]]
  <tr>
    <td>NMC1034
    <td>NXT Compass Sensor
    <td>I2C/M
    <td>Y
    <td>[[ht-nmc1034]]
  <tr>
    <td>NMS1035
    <td>NXT Magnetic Sensor
    <td>Analog/NXT
    <td>Y*
    <td>
  <tr>
    <td>NSK1042
    <td>NXT IRSeeker V2
    <td>I2C/M
    <td>Y
    <td>[[ht-nsk1042]]
  <tr>
    <td>NSX2020
    <td>NXT Sensor Multiplexer
    <td>I2C/M
    <td>Y
    <td>[[ht-nsx2020]]
  <tr>
    <td>NTX1060
    <td>NXT Touch Sensor Multiplexer
    <td>Analog/NXT
    <td>Y*
    <td>
  <tr>
    <td>SPR2010
    <td>NXT SuperPro Prototype Board
    <td>I2C/M
    <td>Y
    <td>[[ht-spr2010]]
  <tr>
    <td>???
    <td>NXT Color Sensor (v1)
    <td>I2C/M
    <td>Y
    <td>[[ht-nco]]
  <tr>
    <td rowspan="12"><a href="http://lego.com">LEGO</a> / <a href="http://education.lego.com">LEGO&nbsp;Education</a>
    <td>9668
    <td>Energy Display
    <td>I2C/M
    <td>Y
    <td>[[lego-9668]]
  <tr>
    <td>9694
    <td>NXT Color Sensor
    <td>Special
    <td>Y
    <td>[[nxt-color-sensor]]
  <tr>
    <td>9749
    <td>NXT Temperature Sensor
    <td>I2C/S
    <td>N
    <td>[[tmp275]]
  <tr>
    <td>9843
    <td>NXT Touch Sensor
    <td>Analog/NXT
    <td>Y
    <td>[[nxt-touch-sensor]]
  <tr>
    <td>9844
    <td>NXT Light Sensor
    <td>Analog/NXT
    <td>Y
    <td>
  <tr>
    <td>9845
    <td>NXT Sound Sensor
    <td>Analog/NXT
    <td>Y*
    <td>
  <tr>
    <td>9846
    <td>NXT Ultrasonic Sensor
    <td>I2C/M
    <td>Y
    <td>[[lego-9846]]
  <tr>
    <td>45504
    <td>EV3 Ultrasonic Sensor
    <td>UART
    <td>Y
    <td>[[legoev3-uart]]
  <tr>
    <td>45505
    <td>EV3 Gyro Sensor
    <td>UART
    <td>Y
    <td>[[legoev3-uart]]
  <tr>
    <td>45506
    <td>EV3 Color Sensor
    <td>UART
    <td>Y
    <td>[[legoev3-uart]]
  <tr>
    <td>45507
    <td>EV3 Touch Sensor
    <td>Analog/EV3
    <td>Y
    <td>[[ev3-touch-sensor]]
  <tr>
    <td>45509
    <td>EV3 Infrared Sensor
    <td>UART
    <td>Y
    <td>[[legoev3-uart]]
  <tr>
    <td rowspan="1"><a href="http://www.LogITNXT.com">LogIT</a>
    <td>
    <td>NXT Sensor Adapter
    <td>
    <td>
    <td>
  <tr>
    <td rowspan="5"><a href="http://www.mindsensors.com">mindsensors.com</a>
    <td>LightSensorArray
    <td>Light Sensor Array
    <td>I2C/M
    <td>Y
    <td>[[ms-light-array]]
  <tr>
    <td>MagicWand
    <td>Magic Wand Kit
    <td>I2C/S
    <td>N
    <td>[[pcf8574]]
  <tr>
    <td>PCF8574-Nx
    <td>Sensor building kit for NXT with PCF8574 IC
    <td>I2C/S
    <td>N
    <td>[[pcf8574]]
  <tr>
    <td>PCF8591-Nx
    <td>Sensor building kit for NXT with PCF8591 IC
    <td>I2C/S
    <td>N
    <td>[[pcf8591]]
  <tr>
    <td>RTC-Nx-v3
    <td>Realtime Clock for NXT 
    <td>I2C/S
    <td>N
    <td>[[ds1307]]
  <tr>
    <td rowspan="1"><a href="http://www.vernier.com">Vernier</a>
    <td>
    <td>NXT Sensor Adapter
    <td>
    <td>
    <td>
</table>
\* Analog/NXT sensors are detected but cannot be differentiated, so a generic interface is provided. Additional drivers may be required (although none exist yet).