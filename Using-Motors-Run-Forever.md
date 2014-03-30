
## DRAFT - DO NOT USE THESE NOTES YET

This page introduces the fundamental `run_forever` mode of the `ev3dev` motor driver.  It's part of a series of wiki pages that describe using motors with the EV3 running `ev3dev` that includes:

-  [Using Motors](https://github.com/mindboards/ev3dev/wiki/Using-Motors)
-  [Using Motors - Run Forever](https://github.com/mindboards/ev3dev/wiki/Using-Motors-Run-Forever)

## Known issues

## Overview

The simplest `ev3dev` motor driver operation is the so-called `run_forever` mode. You specify the  `setpoint` attribute and the motor driver controls the motor until you tell it to stop. You can also use the `regulate` attribute to affect how the driver handles changes in motor speed due to loading.

### Tacho Motor Run Mode

The `run_mode` attribute determines how the motor is going to run. The default `run_mode` when you plug in a motor is `forever` - which is exactly what we need here. Read the current `run_mode` of your motor to be sure it's set correctly. If it's anything other than `forever`, just unplug the motor for a few seconds and plug it in again to reset it.

```
user@ev3dev:~$ cat /sys/class/tacho-motor/outB:motor:tacho/run_mode
forever
```

### Tacho Motor Speed Setpoint

The `speed_setpoint` attribute can range from -100 to +100, values outside this range result in an error when you try to write. Here's an example of valid and invalid writes to the `speed_setpoint` attribute:

```
user@ev3dev:~$ echo -10 > /sys/class/tacho-motor/outB:motor:tacho/speed_setpoint
user@ev3dev:~$ echo  10 > /sys/class/tacho-motor/outB:motor:tacho/speed_setpoint
user@ev3dev:~$ echo  50 > /sys/class/tacho-motor/outB:motor:tacho/speed_setpoint
user@ev3dev:~$ echo 101 > /sys/class/tacho-motor/outB:motor:tacho/speed_setpoint
-bash: echo: write error: Invalid argument
```

Of course, you can read the `speed_setpoint` back using the by-now familiar `cat` command:

```
user@ev3dev:~$ cat /sys/class/tacho-motor/outB:motor:tacho/speed_setpoint
50
```

Yep, that was the last reasonable value that was set!

### Tacho Motor Run

The `run` attribute is a numerical value - 0 means stop, anthing else means run

Maybe this should also be a text attribute?

Here we will force the motor to run at the desired `speed_setpoint` forever. You can update the `speed_setpoint` while the motor is running.


```
user@ev3dev:~$ echo  50 > /sys/class/tacho-motor/outB:motor:tacho/speed_setpoint
user@ev3dev:~$ echo   1 > /sys/class/tacho-motor/outB:motor:tacho/run
user@ev3dev:~$ echo  60 > /sys/class/tacho-motor/outB:motor:tacho/speed_setpoint
user@ev3dev:~$ echo -40 > /sys/class/tacho-motor/outB:motor:tacho/speed_setpoint
```

You can read the position, speed, and state of the motor too:

```
user@ev3dev:~$ cat /sys/class/tacho-motor/outB:motor:tacho/state
run_forever
user@ev3dev:~$ cat /sys/class/tacho-motor/outB:motor:tacho/speed
-29
user@ev3dev:~$ cat /sys/class/tacho-motor/outB:motor:tacho/power
-40
user@ev3dev:~$ cat /sys/class/tacho-motor/outB:motor:tacho/position
-9044
```

And of course, you can stop the motor by writing 0 to the `run` attribute.

```
user@ev3dev:~$ echo 0 > /sys/class/tacho-motor/outB:motor\:tacho/run
user@ev3dev:~$ cat /sys/class/tacho-motor/outB:motor:tacho/state
idle
```

The motor should gently "coast" to a stop. We'll discuss making the motor "brake" instead of coast after we talk a bit about nregulation.

### Tacho Motor Regulation Mode

If you run the motor at a fairly low speed setpoint as described above, and you try to stop the hub of the motor with your thumb, you'll find it's pretty easy to slow down or even stop the motor.

Because we are running with default values, the motor driver just sets the power to the motor according to the speed setpoint, and leaves it there.

In some cases, this is not what you want. You want the motor to "try harder" when it encounters resistance - and the `regulation_mode` attribute is going to help us with that.

