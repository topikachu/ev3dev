### General
- Type ID: 33
- Modes: 6

### Mode 0
- Name: IR-PROX
- Number of measured values: 1
- Value 0: Proximity (distance)
- Units: pct (percentage)
- Min: 0 (very close)
- Max: 100 (far away - approx. 70cm/27in)

### Mode 1
- Name: IR-SEEK
- Number of measured values: 8
- Value 0: Channel 1 Heading
- Value 1: Channel 1 Proximity
- Value 2: Channel 2 Heading
- Value 3: Channel 2 Proximity
- Value 4: Channel 3 Heading
- Value 5: Channel 3 Proximity
- Value 6: Channel 4 Heading
- Value 7: Channel 4 Proximity
- Units: pct (percentage)
- Heading Min: -25 (far left)
- Heading Max: 25 (far right)
- Proximity Min: 0 (very close)
- Proximity Max: 100 (far away - approx. 200cm/79in)

Note on Mode 1: The absence of a beacon on a channel can be detected when Proximity == -128 (and heading == 0).

### Mode 2
- Name: IR-REMOTE
- Number of measured values: 4
- Value 0: Channel 1
- Value 1: Channel 2
- Value 2: Channel 3
- Value 3: Channel 4
- Units: btn (button)
    - 0: none
    - 1: red up
    - 2: red down
    - 3: blue up
    - 4: blue down
    - 5: red up and blue up
    - 6: red up and blue down
    - 7: red down and blue up
    - 8: red down and blue down
    - 9: beacon mode on
    - 10: red up and red down
    - 11: blue up and blue down
- Min: 0 (none)
- Max: 11 (blue up and blue down)

Notes on Mode 2: Pressing more that 2 buttons at one time is not supported. It will usually read 0. Pressing an up/down button while beacon mode is activated with turn off beacon mode.

### Mode 3
- Name: IR-REM-A
- Number of measured values: 1
- Value 0: Channel 1

    | Value   | Blue Down | Blue Up | Red Down | Red Up |
    |:-------:|:---------:|:-------:|:--------:|:------:|
    | 262/384 |           |         |          |        |
    | 287     |           |         |          | X      |
    | 300     |           |         | X        |        |
    | 309     |           |         | X        | X      |
    | 330     |           | X       |          |        |
    | 339     |           | X       |          | X      |
    | 352     |           | X       | X        |        |
    | 377     |           | X       | X        | X      |
    | 390     | X         |         |          |        |
    | 415     | X         |         |          | X      |
    | 428     | X         |         | X        |        |
    | 437     | X         |         | X        | X      |
    | 458     | X         | X       |          |        |
    | 467     | X         | X       |          | X      |
    | 480     | X         | X       | X        |        |
    | 505     | X         | X       | X        | X      |

- Units: _none_
- Min: 0
- Max: 65535???

Notes on Mode 3: The MSB is always 0x01. In the LSB, the 4 most significant bits represent each button. Bit 7 is the blue down button, bit 6 is the blue up button, bit 5 is the red down button, bit 4 is the red up button. Beware that when no buttons are pressed, bit 7 is set (value == 384). You can test that bits 0-3 are all 0 to check this. Also, when the beacon mode is active or for about 1 second after any button is released the value is 262. This only works with the remote on channel 1.

```C
if ((value & 0x0F) == 0) {
    // no buttons are pressed
} else {
    if (value & 0x80)
        // blue down button is pressed
    if (value & 0x40)
        // blue up button is pressed
    if (value & 0x20)
        // red down button is pressed
    if (value & 0x10)
        // red up button is pressed
}
```

Bits 0-3 seem to be some sort of checksum or parity check. Bit 0 = bit 4, bit 1 = ~(bit 5), bit 2 = ~(bit 6), bit 3 = 0 if bits 0-2 are even or 1 if bits 0-2 are odd.

### Mode 4
- Name: IR-S-ALT
- Number of measured values: 4
- Value 0: ???
- Value 1: ???
- Value 2: ???
- Value 3: ???
- Units: pct
- Min: 0 (???)
- Max: 100 (???)

Notes on Mode 4: This mode does not seem to be usable. When switching to this mode, the sensor quits responding to the keep-alive messages and the sensor resets.

### Mode 5
- Name: IR-CAL
- Number of measured values: 2
- Value 0: ???
- Value 1: ???
- Units: _none_
- Min: 0
- Max: 1023

Notes on Mode 5: Not sure how this mode is supposed to work. Probably have to write some data to the sensor. Values return 0.