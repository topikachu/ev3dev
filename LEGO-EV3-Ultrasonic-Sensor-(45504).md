### General

| Type ID | Modes |
|:-------:|:-----:|
| 30      | 7     |

### Modes

|             | Mode 0 | Mode 1 | Mode 2 | Mode 3 | Mode 4 | Mode 5 | Mode 6 |
|-------------|--------|--------|--------|--------|--------|--------|--------|
| Name        | US-DIST-CM | US-DIST-IN | US-LISTEN | US-SI-CM | US-SI-IN | US-DC-CM | US-DC-IN
| Description | Continuous measurement | Continuous measurement | Listen | Single measurement | Single measurement | ??? | ???
| # Values    | 1 | 1 | 1 | 1 | 1 | 1 | 1
| Value 0     | Distance | Distance | Presence of another ultrasonic sensor | Distance | Distance | Distance | Distance
| Min         | 0 (0&nbsp;cm) | 0 (0.0&nbsp;in)  | 0 (no other sensors detected) | 0 (0.0&nbsp;cm) | 0 (0.0&nbsp;in) |  0 (0.0&nbsp;cm) | (0.0&nbsp;in)
| Max         | 2550 (255.0&nbsp;cm) | 1003 (100.3&nbsp;in) | 1 (another ultrasonic sensor was detected) | 2550 (255.0&nbsp;cm) | 1003 (100.3&nbsp;in) | 2550 (255.0&nbsp;cm) | 1003 (100.3&nbsp;in)
| Units       | cm (centimeters) | in (inches) | _none_ | cm (centimeters) | in (inches) | cm (centimeters) | in (inches)
| Decimals    | 1 | 1 | 0 | 1 | 1 | 1 | 1
| LED State   | On, steady | On, steady | On, blinking | Off | Off | On, steady | On, steady

Notes on Mode 3/4: SI means SIngle shot mode. The value is read when the mode is set and does not change. To read a new value, set the mode again (e.g. ```echo US-SI-CM > mode```).
