
## DRAFT - DO NOT USE THESE NOTES YET

This page introduces the fundamental `run_forever` mode of the `ev3dev` motor driver.  It's part of a series of wiki pages that describe using motors with the EV3 running `ev3dev` that includes:

-  [Using Motors](https://github.com/mindboards/ev3dev/wiki/Using-Motors)
-  [Using Motors - Run Forever](https://github.com/mindboards/ev3dev/wiki/Using-Motors-Run-Forever)

### Table of Contents

- [Known Issues](#KnownIssues)
- [Overview](#Overview)
- [`run_mode`](#TachoMotorRunMode)
- [`speed_setpoint`](#TachoMotorSpeedSetpoint)
- [`run`](#TachoMotorRun)
- [`regulation_mode`](#TachoMotorRegulationMode)
- [`brake_mode`](#TachoMotorBrakeMode)
- [`hold_mode`](#TachoMotorHoldMode)

### <a name="KnownIssues"/> Known issues

No known Issues at this time

### <a name="Overview"/> Overview

The simplest `ev3dev` motor driver operation is the so-called `run_forever` mode. You specify the  `speed_setpoint` attribute and the motor driver runs the motor until you tell it to stop. You can also use the `regulation_mode` attribute to affect how the driver handles changes in motor speed due to loading.

### <a name="TachoMotorRunMode"/> Tacho Motor `run_mode`

The `run_mode` attribute determines how the motor is going to run. The default `run_mode` when you plug in a motor is `forever` - which is exactly what we need here. Read the current `run_mode` of your motor to be sure it's set correctly. If it's anything other than `forever`, just unplug the motor for a few seconds and plug it in again to reset it.

```
user@ev3dev:~$ cat /sys/class/tacho-motor/outB:motor:tacho/run_mode
forever
```

### <a name="TachoMotorSpeedSetpoint"/>Tacho Motor `speed_setpoint`

The `speed_setpoint` attribute can range from -100 to +100, values outside this range result in an error when you try to write. As mentioned in the [Using Motors](https://github.com/mindboards/ev3dev/wiki/Using-Motors) wiki page, the `speed_setpoint` does not actually represent the speed of the motor. Think of it more in terms of a percentage of the theoretical maximum speed.

Here's an example of valid and invalid writes to the `speed_setpoint` attribute:

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

### <a name="TachoMotorRun"/>Tacho Motor `run`

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
user@ev3dev:~$ echo 0 > /sys/class/tacho-motor/outB:motor:tacho/run
user@ev3dev:~$ cat /sys/class/tacho-motor/outB:motor:tacho/state
idle
```

The motor should gently "coast" to a stop. We'll discuss making the motor "brake" instead of coast after we talk a bit about regulation.

### <a name="TachoMotorRegulationMode"/>Tacho Motor `regulation_mode`

If you run the motor at a fairly low `speed_setpoint` as described above, and you try to stop the hub of the motor with your thumb, you'll find it's pretty easy to slow down or even stop the motor. Because we are running with default values, the motor driver just sets the power to the motor according to the `speed_setpoint`, and leaves it there.

In some cases, this is not what you want. You want the motor to "try harder" when it encounters resistance - and the `regulation_mode` attribute is going to help us with that.

The `regulation_mode` attribute has two possible values `on` and `off` - the default is `off`. To turn on regulation, all you need to do is write `on` to the `regulation_mode` attribute, like this:

```
user@ev3dev:~$ cat /sys/class/tacho-motor/outB:motor:tacho/regulaton_mode
off
user@ev3dev:~$ echo on > /sys/class/tacho-motor/outB:motor:tacho/regulation_mode
user@ev3dev:~$ cat /sys/class/tacho-motor/outB:motor:tacho/regulaton_mode
on
```

Now turn on the motor and try to slow the hub down with your thumb. Notice how the motor tries harder to maintain the `speed_setpoint`? That's a very useful tweak to your robot if you find the mechnaism stalls.

Regulation also helps when the batteries start running low. Remember that the `speed_setpoint` in unregulated mode just sends a percentage of the battery voltage to the motor. When the batteries get depleted, the percentage stays the same but the resulting voltage at the motor goes down in proportion to the battery, and the motor will run slower.

Turning regulation on in this case will make the EV3 driver the ports a little harder to compensate for the lower battery voltage to try and keep the speed at the `speed_setpoint`.

You can turn `regulation_mode` off and on while the motor is running if you need to.

### <a name="TachoMotorBrakeMode"/>Tacho Motor `brake_mode`

In a previous section we talked about how the motor tends to "coast" to a stop if you turn it off suddenly. for some kinds of robots, a more precise method of stopping is needed - and that's where the `brake_mode` attribute comes in.

Once again, this is an `on` and `off` attribute. The default value of `brake_mode` is `off`. When the motor is turned off, the internal H-bridge that drives the motors is left in a state where there is no load applied to the motor. When you set the `brake_mode` attribute to `on`, the H-bridge applies a short across the motor terminals.

To see the effect of this in action, turn the hub of the motor when it is disconnected from the brick. Note the relative ease of turning the hub, and how it coasts after you stop spinning it.

Now attach the standard tacho motor to the other tacho motor in the kit, using one of the connection cables. Turn on of the motor hubs. Did you notice that it was a bit harder to turn? Did you notice that the hub of the other motor turned too? That's the effect of a motor in generator mode. Applying energy to the output of the motor (turning the hub) results in electricity being generated by the motor!

Now hold the hub of the one motor in fixed position while turning the hub of the other motor. Notice that the hub is much harder to turn now, and no longer "coasts" to a stop.

```
user@ev3dev:~$ cat /sys/class/tacho-motor/outB:motor:tacho/brake_mode
off
user@ev3dev:~$ echo on > /sys/class/tacho-motor/outB:motor:tacho/brake_mode
user@ev3dev:~$ cat /sys/class/tacho-motor/outB:motor:tacho/brake_mode
on
```

You can update the `brake_mode` even while the motor is running, but you won't see its effect until the motor stops.

### <a name="TachoMotorHoldMode"/>Tacho Motor `hold_mode`

The final basic attribute is `hold_mode`. Just like the `brake_mode` attribute, the `hold_mode` can be either `off` or `on` - the default setting is `off`.

Where the `brake_mode` attribute improves the ability of the motor to stop quickly, the `hold_mode` does it one better. This attribute is used to control if the motor holds its position after it has been turned off.

Be careful, this can consume quite a bit of power if you are trying to hold a large load stationary. There may need to be a new attribute added that controls how hard the motor tries to control position, but let's wait and see.

Note that this is the only attribute that has any effect on the motor when the motor `run` attribute is '0' - so you can test it right away. Enter the following commands if your motor is plugged in to Motor Port B, and then try and turn the motor hub!

```
user@ev3dev:~$ cat /sys/class/tacho-motor/outB:motor:tacho/hold_mode
off
user@ev3dev:~$ echo on > /sys/class/tacho-motor/outB:motor:tacho/hold_mode
user@ev3dev:~$ cat /sys/class/tacho-motor/outB:motor:tacho/hold_mode
on
```
