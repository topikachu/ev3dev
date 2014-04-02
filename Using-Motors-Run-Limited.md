
## DRAFT - DO NOT USE THESE NOTES YET

This page introduces the `ramp_time` and `ramp_position` modes of the `ev3dev` motor driver.  It's part of a series of wiki pages that describe using motors with the EV3 running `ev3dev` that includes:

-  [Using Motors](https://github.com/mindboards/ev3dev/wiki/Using-Motors)
-  [Using Motors - Run Forever](https://github.com/mindboards/ev3dev/wiki/Using-Motors-Run-Forever)
-  [Using Motors - Run Limited](https://github.com/mindboards/ev3dev/wiki/Using-Motors-Ramping)

### Table of Contents

- [Known Issues](#Known Issues)
- [Overview](#Overview)
- [`run_mode` = `time`](RunModeTime)
- [`time_setpoint`](TimeSetpoint)

### <a name="Known Issues"/> Known issues

No known Issues at this time

### <a name="Overview"/> Overview

While the `run_forever` mode is useful, sometimes you want to tell the system to run a motor for a fixed amount of time, or to some specific position. It's relatively easy to run at full power for n milliseconds, but that's not always helpful. Some robot mechanisms do not react well to being yanked up to full speed and then brought to an abrupt halt.

For these cases, a more general mode of operation that includes a ramp-up to a specified speed, and then a ramp-down to zero has been developed. In fact, there are 2 ramp-enabled `run_mode`s. The first is `time` and the second is `position`.

We'll start with the `run_mode` = `time` description, then move on to a general description of how the `ramp_up` and `ramp_down` attributes are defined, and close out the note with `runmode` = `position`.

### <a name="RunModeTime"/> `run_mode` = `time`

The `run_mode` attribute default is `forever`, but you can simply write `time` to it. So let's go ahead and do that to get started.

```
user@ev3dev:~$ echo time > /sys/class/tacho-motor/outB:motor:tacho/run_mode
user@ev3dev:~$ echo 40   > /sys/class/tacho-motor/outB:motor:tacho/speed_setpoint
user@ev3dev:~$ echo 1    > /sys/class/tacho-motor/outB:motor:tacho/run
```

What happened? Nothing. That's because we have not told the motor how long it should run for yet!

### <a name="TimeSetpoint"/> `time_setpoint`

We have gone over the `speed_setpoint` in a previous section, and it's used to set the speed of the motor. Recall that it's not actually the speed - it's more like a percentage of maximum speed of the motor.

It stands to reason that there will need to be an attribute that tells the motor driver how long it should run for, and that's exactly what `time_setpoint` does for us. As soon as we set a value and tell the motor to run, it will run for `time_setpoint` milliseconds from that point in time.

```
user@ev3dev:~$ echo 2000 > /sys/class/tacho-motor/outB:motor:tacho/time_setpoint
user@ev3dev:~$ echo 1    > /sys/class/tacho-motor/outB:motor:tacho/run
```

Nice! The motor runs for exactly 2 seconds - but it coasts to a stop. We know how to fix that.

```
user@ev3dev:~$ echo on > /sys/class/tacho-motor/outB:motor:tacho/brake_mode
user@ev3dev:~$ echo 1  > /sys/class/tacho-motor/outB:motor:tacho/run
```

And note that the setpoint does not change, even after the run. That means you can easily tell the motor to run for the same amount of time without having to reload the time_setpoint.



