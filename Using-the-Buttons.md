The buttons on the EV3 are mapped as regular keyboard keys. UP, DOWN, LEFT, RIGHT, ENTER and ESC.

TODO: add photo.

Try this to see that they are working.
```sh
root@ev3dev:/sys/class/leds# hexdump -e '"timestamp:%d.%d""\t""" 1/2 "type:%i""\t"""  1/2 "code:%3i""\t"""  "value:%d\n"' < /dev/input/by-path/platform-gpio-keys.0-event 
timestamp:1391366282.119886	type:1	code:  1	value:0
timestamp:1391366282.120100	type:0	code:  0	value:0
timestamp:1391366282.829942	type:1	code:  1	value:1
timestamp:1391366282.830179	type:0	code:  0	value:0
timestamp:1391366284.300099	type:1	code:105	value:0
timestamp:1391366284.300319	type:0	code:  0	value:0
timestamp:1391366284.829989	type:1	code:105	value:1
timestamp:1391366284.830223	type:0	code:  0	value:0
timestamp:1391366286.19866	type:1	code:103	value:0
timestamp:1391366286.20076	type:0	code:  0	value:0
timestamp:1391366286.319967	type:1	code:103	value:1
timestamp:1391366286.320202	type:0	code:  0	value:0
timestamp:1391366287.169925	type:1	code:106	value:0
timestamp:1391366287.169973	type:0	code:  0	value:0
timestamp:1391366287.479994	type:1	code:106	value:1
timestamp:1391366287.480234	type:0	code:  0	value:0
timestamp:1391366288.339882	type:1	code: 28	value:0
timestamp:1391366288.340092	type:0	code:  0	value:0
timestamp:1391366288.699929	type:1	code: 28	value:1
timestamp:1391366288.700291	type:0	code:  0	value:0
timestamp:1391366289.470046	type:1	code:108	value:0
timestamp:1391366289.470263	type:0	code:  0	value:0
timestamp:1391366289.829943	type:1	code:108	value:1
timestamp:1391366289.830176	type:0	code:  0	value:0
^C
```