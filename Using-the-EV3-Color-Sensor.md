### General
- Type ID: 29
- Modes: 6

### Mode 0
- Name: COL-REFLECT
- Number of measured values: 1
- Value 0: Reflected light intensity
- Units: pct (percentage)
- Min: 0 (no reflected light detected)
- Max: 100 (maximum reflected light detected)
- LED state: Red LED on

### Mode 1
- Name: COL-AMBIENT
- Number of measured values: 1
- Value 0: Ambient light intensity
- Units: pct (percentage)
- Min: 0 (no ambient light detected)
- Max: 100 (maximum ambient light detected)
- LED state: Blue LED on

### Mode 2
- Name: COL-COLOR
- Number of measured values: 1
- Value 0: Detected color
- Units: col (color)
    - 0: none - sensor too close to object
    - 1: black
    - 2: blue
    - 3: green
    - 4: yellow
    - 5: red
    - 6: white
    - 7: brown
- Min: 0 (none)
- Max: 7 (brown)
- LED state: Rapidly cycles red green and blue. Appears white or "rainbow".


### Mode 3
- Name: REF-RAW
- Number of measured values: 2
- Value 0: Reflected/Ambient light intensity???
- Value 1: Reflected/Ambient light intensity???
- Units: none
- Min: 0 (???)
- Max: 1020 (???)
- LED state: Red LED on

### Mode 4
- Name: RGB-RAW
- Number of measured values: 3
- Value 0: Reflected red light intensity???
- Value 1: Reflected green light intensity???
- Value 2: Reflected blue light intensity???
- Units: none
- Min: 0 (???)
- Max: 1020 (???)
- LED state: LED state: Rapidly cycles red green and blue. Appears white or "rainbow".

### Mode 5
- Name: COL-CAL
- Number of measured values: 4
- Value 0: ???
- Value 1: ???
- Value 2: ???
- Value 3: ???
- Units: none
- Min: 0 (???)
- Max: 65535 (???)
- LED state: LED state: Rapidly cycles red green and blue. Appears white or "rainbow".

Note on COL-CAL: When in COL-CAL mode, the color sensor does not respond to the keep-alive sent from the EV3 brick. As a result, the sensor will time out and reset after 1-2 seconds in COL-CAL mode. When using this mode, you should set the mode, do what you need to and change back to another mode within 1 second. Of course, LMS2012 does not appear to use this mode when "calibrating" the color sensor, so it may prove to be useless anyway.