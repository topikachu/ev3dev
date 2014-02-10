## Kinds of I2C Devices

The I2C standards only specify how data is sent from device to device. It does not specify the layout of the registers of a device. LEGO, however, has guidelines for 3rd party manufactures so that they can provide sensors with uniform register layout.

We call sensors that were designed following LEGO's guidelines **I2C/M** sensors (M is for Mindstorms). This common interface lets us autodetect the type of sensor and proved access to the sensor via the ```msensor``` class.

We refer to sensors that do not conform to LEGO's specifications as **I2C/S** sensors (S is for Standard). There are so many types of I2C chips in the wild that are already supported on Linux, that we do not attempt to autodetect them. To use them, we have to find a compatible driver and manually load it.

## Using I2C/M Sensors

See [[Using the Mindstorms Sensor Device Class]] for general usage. This is the I2C specific usage.

To be continued...