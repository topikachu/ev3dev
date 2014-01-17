The EV3 uses a Texas Instruments ADS7957 16 channel 10-bit analog digital converter chip. It is connected to the CPU via [SPI](EV3 SPI). We are using the 5V input mode (i.e. 1024 == 5.00V).

##Documentation
* [Datasheet (pdf)](http://www.ti.com/lit/ds/symlink/ads7957.pdf)

##Channel Usage
<table border="1">
<tr><th>Ch.<th>Connection<th>Notes
<tr><td>0<td>Output port B pin 5<td>
<tr><td>1<td>Output port A pin 5<td>
<tr><td>2<td>N/C<td>Was battery temperature on pre-release hardware
<tr><td>3<td>Battery current<td>Uses 0.05&#8486; shunt resistor, value read is 15x actual voltage
<tr><td>4<td>Battery voltage<td>Value read is 1/2 actual voltage
<tr><td>5<td>Input port 1 pin 6<td>
<tr><td>6<td>Input port 1 pin 1<td>
<tr><td>7<td>Input port 2 pin 6<td>
<tr><td>8<td>Input port 2 pin 1<td>
<tr><td>9<td>Input port 3 pin 6<td>
<tr><td>10<td>Input port 3 pin 1<td>
<tr><td>11<td>Input port 4 pin 6<td>
<tr><td>12<td>Input port 4 pin 1<td>
<tr><td>13<td>Output port C pin 5<td>
<tr><td>14<td>Output port D pin 5<td>
<tr><td>15<td>N/C<td>Was motor current on pre-release hardware
</table>

##Notes
In lsm2012, you will see scaling of the value read from the ADC by 4096 (12-bits) instead of by 1024 (10-bits). This is because they are not shifting the value read to the right 2 bits. Since this is a 10-bit chip, the 2 least significant bits read will always be 0.