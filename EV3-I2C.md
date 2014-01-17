The [AM1808 SoC](EV3 Processor) has 2 hardware [Inter-Integrated Circuit](https://en.wikipedia.org/wiki/I2c) (I2C) controllers. Additionally, there are 4 software controllers implemented using [fast interrupts](EV3 FIQ) (FIQs).

##USAGE
__I2C0__: [Boot and bluetooth EEPROMs](EV3 EEPROM) @400kHz

__I2C0__: Not used/connected

__FIQ I2C__: [Input ports 1-4](EV3 FIQ) @10kHz