### Essentials
* Texas Instruments AM1808 ARM Microporcessor
* 32-bit
* ARM9
* All internal pullup/pulldown resistors are disabled

### Documentation
* [Official Website](http://www.ti.com/product/am1808)
* [AM1808 ARM® Microprocessor Datasheet (pdf)](http://www.ti.com/lit/ds/sprs653d/sprs653d.pdf)
* [AM1808 Technical Reference Manual (pdf)](http://www.ti.com/lit/ug/spruh82a/spruh82a.pdf)
- [AM1808 Pinmux Utility (pdf)](http://www.ti.com/lit/an/spraba2a/spraba2a.pdf)

### System Components
#### Used by EV3
* 3 - [16550-Type UART Modules](EV3 UART)
* 2 - [Serial Peripheral Interfaces (SPI)](EV3 SPI)
* 2 - [Multimedia Card (MMC)/Secure Digital (SD) Card Interfaces](EV3 SD Card Reader) (using one)
* 2 - [Master/Slave I2C Interfaces](EV3 I2C) (using one)
* [Programmable Real-Time Unit Subsystem (PRUSS)](EV3 PRU)
* [USB 1.1 Host Port (OHCI)](EV3 USB Host Port)
* [USB 2.0 On-The-Go Port (OTG)](EV3 PC USB Port)
* [Real-Time Clock (RTC)](EV3 RTC)
* 1 - [64-bit General-Purpose or Watchdog Timer](EV3 FIQ I2C)
* 2 - [Enhanced High-Resolution Pulse Width Modulators (eHRPWM)](EV3 PWM)
* 3 - [32-bit Enhanced Capture Modules (ePCAP)](EV3 PWM)

#### Not used by EV3
* LCD Controller (EV3 uses an [external controller](EV3 LCD Display))
* 1 - Host Port Interface (HPI)
* 1 - Multichannel Audio Serial Port (EV3 uses [PWM for sound](EV3 PWM))
* 2 - Multichannel Buffered Serial Ports
* 10/100 Mbps Ethernet MAC (EMAC)
* Video Port Interface (VPIF)
* Universal Parallel Port (uPP)
* Serial ATA (SATA) Controller

#### Not sure yet
* Enhanced Direct Memory Access Controller 3 (EDMA3)
* 3 - 64-bit General-Purpose Timers

### Pin Assignments
There are 400 pins on the chip. The pins are multiplexed so that each pin can perform multiple functions. This is how the EV3 uses each pin. See section 10.4.9 in the technical reference manual to see where this came from.

Most of the "?" pins are probably not connected to anything. We will find out for sure if/when LEGO releases schematics.

<table">
<tr><th colspan="2">MUX<th>Function<th>Usage<th colspan="2">MUX<th>Function<th>Usage
<tr><td rowspan="8">0<td>28<td>UART2&nbsp;CTS<td>Bluetooth<td rowspan="8">1<td>28<td>ECAP1&nbsp;APWM1<td>Output Port D Motor Driver
<tr><td>24<td>UART2&nbsp;RTS<td>Bluetooth<td>24<td>GPIO&nbsp;0-1<td>Input Port 4 Pin 5 I/O
<tr><td>20<td>?<td><td>20<td>GPIO&nbsp;0-2<td>Input Port 1 Pin 5 I/O
<tr><td>16<td>?<td><td>16<td>GPIO&nbsp;0-3<td>Output Port B Pin 1 In
<tr><td>12<td>GPIO&nbsp;0-12<td>Input Port 3 Pin 5 I/O<td>12<td>GPIO&nbsp;0-4<td>Output Port A Pin 6 In
<tr><td>8<td>GPIO&nbsp;0-13<td>Input Port 2 Pin 6 I/O<td>8<td>?<td>
<tr><td>4<td>GPIO&nbsp;0-14<td>Input Port 2 Pin 5 I/O<td>4<td>GPIO&nbsp;0-6<td>A/D Converter Battery Enable (switches battery voltage to ADC channel 4)
<tr><td>0<td>GPIO&nbsp;0-15<td>Input Port 1 Pin 6 I/O<td>0<td>ECAP2&nbsp;APWM2<td>Bluetooth Clock
<tr><td rowspan="8">2<td>28<td>ECAP0&nbsp;APWM0<td>Output Port C Motor Driver<td rowspan="8">3<td>28<td>?<td>
<tr><td>24<td>AXR1<td>Input Port 4 Pin 6 UART RXD<td>24<td>SPI0&nbsp;CS<td>SPI chip select to analog/digital converter
<tr><td>20<td>AXR2<td>Input Port 3 Pin 6 UART RXD<td>20<td>UART0&nbsp;TXD/<br>GPIO&nbsp;8-3<td>Input Port 2 Pin 5 UART TXD/I2C Clock
<tr><td>16<td>AXR3/<br>GPIO&nbsp;1-11<td>Input Port 4 Pin 5 UART TXD/I2C Clock<td>16<td>UART0&nbsp;RXD<td>Input Port 2 Pin 6 UART RXD
<tr><td>12<td>AXR4/<br>GPIO&nbsp;1-12<td>Input Port 3 Pin 5 UART TXD/I2C Clock<td>12<td>SPI0&nbsp;SIMO<td>SPI data from analog/digital converter
<tr><td>8<td>GPIO&nbsp;1-13<td>Button 1 (Enter)<td>8<td>SPI0&nbsp;SOMI<td>SPI data to analog/digital converter
<tr><td>4<td>GPIO&nbsp;1-14<td>Input Port 3 Pin 6 I/O<td>4<td>EPWM0B<td>PWM to speaker amplifier
<tr><td>0<td>GPIO&nbsp;1-15<td>Input Port 4 Pin 6 I/O<td>0<td>SPI0&nbsp;CLK<td>SPI Clock to analog/digital converter
<tr><td rowspan="8">4<td>28<td>UART1&nbsp;TXD/<br>GPIO&nbsp;1-0<td>Input Port 1 Pin 5 UART TXD/I2C Clock<td rowspan="8">5<td>28<td>GPIO&nbsp;2-8<td>Output Port D Pin 6 In
<tr><td>24<td>UART1&nbsp;RXD<td>Input Port 1 Pin 5 UART RXD<td>24<td>GPIO&nbsp;2-9<td>Output Port B Pin 6 In
<tr><td>20<td>UART2&nbsp;TXD<td>Bluetooth<td>20<td>SPI1&nbsp;SIMO<td>LCD SPI data
<tr><td>16<td>UART2&nbsp;RXD<td>Bluetooth<td>16<td>GPIO&nbsp;2-11<td>LCD A0 display data/command selector
<tr><td>12<td>I2C0&nbsp;SDA<td>EEPROM I2C data<td>12<td>GPIO&nbsp;2-12<td>LCD chip select (active low)
<tr><td>8<td>I2C0&nbsp;SCL<td>EEPROM I2C clock<td>8<td>?<td>
<tr><td>4<td>?<td><td>4<td>EPWM1B<td>Output Port A Motor Driver
<tr><td>0<td>?<td><td>0<td>EPWM1A<td>Output Port A Motor Driver
<tr><td rowspan="8">6<td>28<td>?<td><td rowspan="8">7<td>28<td>GPIO&nbsp;3-8<td>Output Port C Pin 5 In
<tr><td>24<td>GPIO&nbsp;2-1<td>Output Port B Pin 2 In<td>24<td>?<td>
<tr><td>20<td>GPIO&nbsp;2-2<td>Input Port 1 Pin 2 In<td>20<td>?<td>
<tr><td>16<td>?<td><td>16<td>?<td>
<tr><td>12<td>?<td><td>12<td>?<td>
<tr><td>8<td>GPIO&nbsp;2-5<td>Output Port B Pin 5 In<td>8<td>?<td>
<tr><td>4<td>?<td><td>4<td>GPIO&nbsp;3-14<td>Output Port C Pin 6 In
<tr><td>0<td>GPIO&nbsp;2-7<td>FIQ shadowing (*was TP4)<td>0<td>GPIO&nbsp;3-15<td>Output Port A Pin 1 In
<tr><td rowspan="8">8<td>28<td>?<td><td rowspan="8">9<td>28<td>?<td>
<tr><td>24<td>?<td><td>24<td>GPIO&nbsp;4-9<td>Bluetooth enable (active low)
<tr><td>20<td>?<td><td>20<td>?<td>
<tr><td>16<td>GPIO&nbsp;3-3<td>Bluetooth PIC enable<td>16<td>?<td>
<tr><td>12<td>?<td><td>12<td>?<td>
<tr><td>8<td>?<td><td>8<td>?<td>
<tr><td>4<td>GPIO&nbsp;3-6<td>Output Port A Pin 2 In<td>4<td>GPIO&nbsp;4-14<td>Bluetooth PIC reset
<tr><td>0<td>?<td><td>0<td>?<td>
<tr><td rowspan="8">10<td>28<td>?<td><td rowspan="8">11<td>28<td>GPIO&nbsp;5-8<td>Output Port B Pin 5 In
<tr><td>24<td>?<td><td>24<td>GPIO&nbsp;5-9<td>Output Port C Pin 2 In
<tr><td>20<td>MMCSD0&nbsp;DAT3<td>SD Card Reader<td>20<td>GPIO&nbsp;5-10<td>Output Port D Pin 1 In
<tr><td>16<td>MMCSD0&nbsp;DAT2<td>SD Card Reader<td>16<td>GPIO&nbsp;5-11<td>Output Port A Pin 5 In
<tr><td>12<td>MMCSD0&nbsp;DAT1<td>SD Card Reader<td>12<td>?<td>
<tr><td>8<td>MMCSD0&nbsp;DAT0<td>SD Card Reader<td>8<td>GPIO&nbsp;5-13<td>Output Port C Pin 5 In
<tr><td>4<td>MMCSD0&nbsp;CMD<td>SD Card Reader<td>4<td>?<td>
<tr><td>0<td>MMCSD0&nbsp;CLK<td>SD Card Reader<td>0<td>GPIO&nbsp;5-15<td>Output Port D Pin 5 In
<tr><td rowspan="8">12<td>28<td>GPIO&nbsp;5-0<td>LCD reset (active low)<td rowspan="8">13<td>28<td>GPIO&nbsp;6-8<td>Output Port C Pin 1 In
<tr><td>24<td>?<td><td>24<td>GPIO&nbsp;6-9<td>Output Port D Pin 5 In
<tr><td>20<td>?<td><td>20<td>GPIO&nbsp;6-10<td>Button 5 (Back)
<tr><td>16<td>GPIO&nbsp;5-3<td>Output Port D Pin 2 In<td>16<td>GPIO&nbsp;6-11<td>System 5V Power (turns off EV3)
<tr><td>12<td>GPIO&nbsp;5-4<td>Output Port A Pin 1 In<td>12<td>GPIO&nbsp;6-12<td>LED 0 (right, red)
<tr><td>8<td>?<td><td>8<td>GPIO&nbsp;6-13<td>LED 2 (left, green)
<tr><td>4<td>?<td><td>4<td>GPIO&nbsp;6-14<td>LED 1 (left, red)
<tr><td>0<td>GPIO&nbsp;5-7<td>Bluetooth CTS<td>0<td>GPIO&nbsp;6-15<td>Speaker amplifier (sound) enable
<tr><td rowspan="8">14<td>28<td>?<td><td rowspan="8">15<td>28<td>?<td>
<tr><td>24<td>?<td><td>24<td>?<td>
<tr><td>20<td>?<td><td>20<td>?<td>
<tr><td>16<td>?<td><td>16<td>?<td>
<tr><td>12<td>?<td><td>12<td>?<td>
<tr><td>8<td>?<td><td>8<td>?<td>
<tr><td>4<td>GPIO&nbsp;6-6<td>Button 4 (left)<td>4<td>?<td>
<tr><td>0<td>GPIO&nbsp;6-7<td>LED 3 (right, red)<td>0<td>?<td>
<tr><td rowspan="8">16<td>28<td>GPIO&nbsp;7-10<td>Input Port 4 buffer enable (active low)<td rowspan="8">17<td>28<td>?<td>
<tr><td>24<td>GPIO&nbsp;7-11<td>Input Port 3 Pin 2 In<td>24<td>?<td>
<tr><td>20<td>GPIO&nbsp;7-12<td>Button 3 (right)<td>20<td>?<td>
<tr><td>16<td>?<td><td>16<td>?<td>
<tr><td>12<td>GPIO&nbsp;7-14<td>Button 2 (down)<td>12<td>?<td>
<tr><td>8<td>GPIO&nbsp;7-15<td>Button 0 (up)<td>8<td>?<td>
<tr><td>4<td>GPIO&nbsp;6-5<td>System power enable (turns off EV3)<td>4<td>GPIO&nbsp;7-8<td>Input Port 4 Pin 2 In
<tr><td>0<td>?<td><td>0<td>GPIO&nbsp;7-9<td>Input Port 3 buffer enable (active low)
<tr><td rowspan="8">18<td>28<td>GPIO&nbsp;8-10<td>Input Port 1 Pin 1 Out<td rowspan="8">19<td>28<td>?<td>
<tr><td>24<td>GPIO&nbsp;8-11<td>Input Port 1 buffer enable (active low)<td>24<td>?<td>
<tr><td>20<td>GPIO&nbsp;8-12<td>Input Port 2 Pin 1 Out<td>20<td>?<td>
<tr><td>16<td>?<td><td>16<td>?<td>
<tr><td>12<td>GPIO&nbsp;8-14<td>Input Port 2 buffer enable (active low)<td>12<td>GPIO&nbsp;6-3<td>USB1 overcurrent
<tr><td>8<td>GPIO&nbsp;8-15<td>Input Port 2 Pin 2 In<td>8<td>GPIO&nbsp;6-4<td>Input Port 4 Pin 1 Out
<tr><td>4<td>?<td><td>4<td>GPIO&nbsp;8-8<td>Rechargable battery indicator
<tr><td>0<td>?<td><td>0<td>GPIO&nbsp;8-9<td>Input Port 3 Pin 1 Out