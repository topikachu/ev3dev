### General
- Type ID: 30
- Modes: 7

### Mode 0
- Name: US-DIST-CM
- Number of measured values: 1
- Value 0: Distance
- Units: cm (centimeters)
- Min: 0 (0 cm)
- Max: 2550 (255.0 cm)
- Decimals: 1
- LED state: On, steady

### Mode 1
- Name: US-DIST-IN
- Number of measured values: 1
- Value 0: Distance
- Units: in (inches)
- Min: 0 (0.0 in)
- Max: 1003 (100.3 in)
- Decimals: 1
- LED state: On, steady

### Mode 2
- Name: US-LISTEN
- Number of measured values: 1
- Value 0: Presence of another ultrasonic sensor
- Units: _none_
- Min: 0 (no other sensors detected)
- Max: 1 (another ultrasonic sensor was detected)
- LED state: On, blinking

### Mode 3
- Name: US-SI-CM
- Number of measured values: 1
- Value 0: Distance
- Units: cm (centimeters)
- Min: 0 (0.0 cm)
- Max: 2550 (255.0 cm)
- Decimals: 1
- LED state: Off

Notes on Mode 3: SI means SIngle shot mode. The value is read only when the mode is set and does not change. To read a new value, set the mode again (e.g. ```echo US-SI-CM > mode```).

### Mode 4
- Name: US-SI-IN
- Number of measured values: 1
- Value 0: Distance
- Units: in (inches)
- Min: 0 (0.0 in)
- Max: 1003 (100.3 in)
- Decimals: 1
- LED state: Off

Notes on Mode 4: SI means SIngle shot mode. The value is read only when the mode is set and does not change. To read a new value, set the mode again (e.g. ```echo US-SI-IN > mode```).

### Mode 5
- Name: US-DC-CM
- Number of measured values: 1
- Value 0: Distance
- Units: cm (centimeters)
- Min: 0 (0.0 cm)
- Max: 2550 (255.0 cm)
- Decimals: 1
- LED state: On, steady

### Mode 6
- Name: US-DC-IN
- Number of measured values: 1
- Value 0: Distance
- Units: in (inches)
- Min: 0 (0.0 in)
- Max: 1003 (100.3 in)
- Decimals: 1
- LED state: On, steady
