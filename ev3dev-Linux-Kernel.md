The ev3dev kernel is based on [Davinci PSP 03.22.00.02](http://processors.wiki.ti.com/index.php/DaVinci_PSP_03.22.00.02_Release_Notes) from TI.


The bleeding edge upstream development for linux-davinci is hosted at [gitorious](https://gitorious.org/linux-davinci/linux-davinci).

#Kernel Drivers
Most, if not all, of the customization of the ev3dev kernel is the addition and patching of hardware drivers for the EV3 specific hardware.

##Where to find stuff
Drivers that implement standard kernel interfaces are located in the appropriate place in the kernel tree. Drivers that don't fit anywhere else are in ```drivers/legoev3/```.

````
$ tree -P "*legoev3*|ev3_*|nxt_*|ms_*|st7586*" -I "*.o|*.ko|*.mod.c|ms_mg.*" --prune
.
├── arch
│   └── arm
│       └── mach-davinci
│           ├── board-legoev3.c
│           ├── board-legoev3.h
│           ├── include
│           │   └── mach
│           │       ├── legoev3-fiq.h
│           │       └── legoev3.h
│           └── legoev3-fiq.c
├── drivers
│   ├── i2c
│   │   └── busses
│   │       └── i2c-legoev3.c
│   ├── legoev3
│   │   ├── ev3_input_port.c
│   │   ├── ev3_touch_sensor.c
│   │   ├── ev3_uart_sensor.c
│   │   ├── legoev3_analog.c
│   │   ├── legoev3_bluetooth.c
│   │   ├── legoev3_ports.c
│   │   ├── legoev3_uart.c
│   │   ├── ms_light_array.c
│   │   ├── nxt_i2c_sensor.c
│   │   ├── nxt_touch_sensor.c
│   │   └── nxt_ultrasonic.c
│   ├── power
│   │   └── legoev3_battery.c
│   └── video
│       └── st7586fb.c
├── include
│   ├── config
│   │   ├── battery
│   │   │   └── legoev3.h
│   │   ├── fb
│   │   │   └── st7586.h
│   │   ├── i2c
│   │   │   └── legoev3.h
│   │   ├── mach
│   │   │   └── davinci
│   │   │       └── legoev3.h
│   │   └── snd
│   │       └── legoev3.h
│   ├── linux
│   │   ├── i2c-algo-legoev3.h
│   │   ├── i2c-legoev3.h
│   │   ├── legoev3
│   │   │   ├── ev3_input_port.h
│   │   │   ├── ev3_output_port.h
│   │   │   ├── legoev3_analog.h
│   │   │   ├── legoev3_bluetooth.h
│   │   │   ├── legoev3_input_port.h
│   │   │   ├── legoev3_ports.h
│   │   │   └── nxt_i2c_sensor.h
│   │   └── power
│   │       └── legoev3_battery.h
│   ├── sound
│   │   └── legoev3.h
│   └── video
│       └── st7586fb.h
└── sound
    └── pwm
        ├── legoev3.c
        └── legoev3.h

````
