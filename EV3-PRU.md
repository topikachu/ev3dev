The [AM1808 SoC](EV3 Processor) has 2 [Independent Programmable Realtime
Unit](http://processors.wiki.ti.com/index.php/Programmable_Realtime_Unit_Subsystem) (PRU) Cores.

## Usage
Using PRU 0 to provide software UART for input ports 3 and 4

## Documentation
* [TI Soft-UART Users guide](http://processors.wiki.ti.com/index.php/Soft-UART_Implementation_on_OMAPL_PRU_-_Software_Users_Guide)

## Firmware
The PRU requires firmware to implement the UART interfaces. We are using the firmware from LEGO (distributed in the [ev3dev-uart](Package-ev3dev-uart) package).

    /lib/firmware/PRU_SUART.bin

## Device Driver
The device driver comes from TI. ev3dev uses one of the copies from lms2012 with minor modifications to make it work in the 3.3 kernel.


