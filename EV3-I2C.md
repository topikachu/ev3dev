The [AM1808 SoC](EV3 Processor) has 2 hardware [Inter-Integrated Circuit](https://en.wikipedia.org/wiki/I2c) (I2C) controllers. Additionally, there are 4 software controllers implemented using [fast interrupts](EV3 FIQ) (FIQs).

## Usage
__I2C0__: [Boot and bluetooth EEPROMs](EV3 EEPROM) @400kHz

__I2C0__: Not used/connected

__[FIQ](EV3 FIQ) I2C__: Input ports 1-4 @10kHz

## Device Drivers
The Linux kernel has a well established [framework for I2C drivers](https://www.kernel.org/doc/Documentation/i2c/).

The SoC I2C uses the existing driver at [drivers/i2c/busses/i2c-davinci.c](https://github.com/mindboards/ev3dev-kernel/blob/master/drivers/i2c/busses/i2c-davinci.c) as a backend.

Since there are not enough I2C controllers on the SoC, LEGO chose to implement the I2C buses for the four input ports using GPIOs. A secondary reason for this is that the NXT Ultrasonic sensors does not work well with standard I2C masters. It requires an extra clock pulse between the stop and the next start. (TODO: add references here.) 

This Linux kernel has an existing GPIO i2c driver, but in order to get the performance needed, we have to use [fast interrupts](EV3 FIQ) (FIQs). (Be sure to follow the link for some interesting reading.) So, the really low level stuff is done in [arch/arm/mach-davinci/legoev3-fiq.c](blob/master/arch/arm/mach-davinci/legoev3-fiq.c) and the rest is in [drivers/i2c/busses/i2c-legoev3.c](blob/master/drivers/i2c/busses/i2c-legoev3.c).

## Sensor Addressing
The I2C bus uses a 7-bit addressing scheme (there is also 10-bit addressing but we are not using it). When sending an address over the bus, the address is shifted to the left 1 bit and the LSB is used to indicate read or write. It is important to know this because LEGO and other 3rd-party sensor manufacturer use the shifted value as the address whereas the linux kernel uses the unshifted value as the address.