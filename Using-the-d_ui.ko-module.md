The EV3 modules that we are distributing all use a "mechanisms, not policy" design paradigm. All the module interaction is done though the `/proc` file on Linux.

Want to set the LEDs to flash a certain way, just write raw data to `/proc/ev3dev_ui`. I won't bore you with every possible language method for reading and writing raw binary data here, there are wiki pages for that on this site. Here's how to do it in bash - yes, you can program a robot in bash!

`echo -n -e \\x10\\x41 > /proc/ev3dev_ui` Flashes left red and right red LEDs alternately
`echo -n -e \\x10\\x42 > /proc/ev3dev_ui` Flashes left green and right red LEDs alternately
`echo -n -e \\x10\\x66 > /proc/ev3dev_ui` Flashes both LEDs read and green alternately
`echo -n -e \\x00\\x00 > /proc/ev3dev_ui` Turns off the annoying flashing LEDs!

I'm sure you can figure out how to turn on the LEDs in any of the built in languages on the EV3, including bash/dash, awk, guile, lua, and python

Here is the documentation for the d_ui.ko driver, straight from the code. Note well that the LEFT button does not work in this driver! For some unknown reason it always returns 1, and as soon as I fix it I will remove this comment.

## Writing to the LEDs

```
/*  The standard LEGO UI driver accepts a single character between '0' and '9'.
 *  The ASCII character '0' is actually 0x30, and '9 is 0x39 - these numbers will
 *  be important shortly.
 *
 *  The Flash pattern is 250mS on, 250mS off
 *  The Pulse pattern is 150mS on, 50mS off, 150mS on, 650mS off
 *
 *  This range of inputs allows for the following 10 standard patterns, the
 *  value on the left is the raw HEX value of the byte to write
 *
 *  0x30 - Steady Black (off)
 *  0x31 - Steady Green
 *  0x32 - Steady Red
 *  0x33 - Steady Orange
 *  0x34 - Flash  Green
 *  0x35 - Flash  Red
 *  0x36 - Flash  Orange
 *  0x37 - Pulse  Green
 *  0x38 - Pulse  Red
 *  0x39 - Pulse  Orange
 *
 * So this is pretty neat, but can we do better? Yes, it turns out that we can
 * get more interesting flash patterns because the left and right LEDs are
 * independently controllable!
 *
 * There are still 3 underlying bit patterns, steady, flash, and pulse. Think
 * of them as 20 bits of on/off data, times 50 msec per interval (which is
 * exactly how they are implemented:
 *
 * Steady : 0000 0000 0000 0000 0000
 * Flash  : 0000 0111 1100 0001 1111
 * Pulse  : 0000 0000 0001 1100 0111
 *
 * We'll define 4 LED colours, which fit neatly into 2 bits each:
 *
 * Black : 00
 * Green : 01
 * Red   : 10
 * Orange: 11
 *
 * We can then put those 2 bits into 4 positions in a byte, as follows:
 *
 * +---------+---------+
 * |  Left   |  Right  | LED Position
 * +----+----+----+----+
 * |  1 |  0 |  1 |  0 | Bit pattern state
 * +----+----+----+----+
 * | 00 | 01 | 10 | 00 | LED Color per state = Black/Green/Red/Black
 * +----+----+----+----+
 *
 * The result would flash the left LED Black/Green and the Right LED Red/Black
 * which would give the impression of an alternating green/red flash pattern!
 *
 * So that fills up the second byte of data, the first byte is either:
 *
 * 0x00 - Steady
 * 0x01 - Flash
 * 0x02 - Pulse
 * 0x03 - LEGO - second byte is ignored
 *
 * Long story short 0x3?0x?? is used for standard LEGO flash patterns
 * The extended patterns are two bytes wide as described above
 */

## Reading the Switches

Reading the switches is accomplished by, you guessed it, reading `/proc/ev3dev_ui` - here's how to do it in bash. Note that this is a toy example, it's here for readability and quick testing.

`cat /proc/ev3dev_ui | od -t x1` Dumps the switch status, one byte per switch.

The switch positions are:

```
0 - UP
1 - ENTER
2 - DOWN
3 - RIGHT
4 - LEFT (currently always returns 1)
5 - BACK

A typical dump from `od` looks like this if the ENTER button is pressed:

$ cat /proc/ev3dev_ui | od -t x1
0000000 00 01 00 00 01 00
0000006
```

Neat!




