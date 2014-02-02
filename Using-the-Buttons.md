The buttons on the EV3 are mapped as regular keyboard keys. UP, DOWN, LEFT, RIGHT, ENTER and ESC.

TODO: add photo.



If you want your program to be event driven, you can read the ```/dev/input/by-path/platform-gpio-keys.0-event``` file. It will block until a key is pressed. The data is in 16 byte blocks. The first 8 bytes are the time stamp (2 unsigned 64-bit integers, seconds and microseconds), the next 2 bytes are the type (unsigned 16-bit integer), the next 2 bytes are the code (unsigned 16-bit integer) and the last 4 bytes are the value (unsigned 32-bit integer).

Here is an example. It prints out 2 lines each time you press a button on the EV3 and 2 more lines each time you release a button. And of course, press CTRL+C to end.

```sh
root@ev3dev:/sys/class/leds# hexdump -e '"timestamp:%d.%6d""\t""" 1/2 "type:%i""\t"""  1/2 "code:%3i""\t"""  "value:%d\n"' < /dev/input/by-path/platform-gpio-keys.0-event 
timestamp:1391366282.119886	type:1	code:  1	value:0
timestamp:1391366282.120100	type:0	code:  0	value:0
timestamp:1391366282.829942	type:1	code:  1	value:1
timestamp:1391366282.830179	type:0	code:  0	value:0
timestamp:1391366284.300099	type:1	code:105	value:0
timestamp:1391366284.300319	type:0	code:  0	value:0
timestamp:1391366284.829989	type:1	code:105	value:1
timestamp:1391366284.830223	type:0	code:  0	value:0
timestamp:1391366286.019866	type:1	code:103	value:0
timestamp:1391366286.020076	type:0	code:  0	value:0
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