## Introduction

Device classes are the hardware abstraction layer used by Linux to separate the useful parts of hardware from the underlying low level implementation. For example, you have a keyboard that is probably USB, but could be bluetooth or maybe even PS/2. They both implement the Linux ```input``` class. Programs that read information from the keyboard only have to know about the ```input``` class. They don't have to know about how to speak USB an bluetooth and PS/2 and every other type of keyboard ever made.

There are so many sensors for the EV3 that it seems natural to do the same thing for ev3dev. Most sensors made for LEGO Mindstorms are very similar in how they work, so as a result, we have the ```msensor``` class.

## sysfs Interface

All device classes in Linux are found at ```/sys/class```. There are quite a few.

```bash
$ cd /sys/class
$ ls
bdi        i2c-adapter  misc          pwm           sound       vc
block      i2c-dev      mmc_host      rtc           spi_master  vtconsole
bluetooth  ieee80211    msensor       scsi_device   tty
firmware   input        mtd           scsi_disk     udc
gpio       leds         net           scsi_generic  uio
graphics   mem          power_supply  scsi_host     usbmon
```

Whenever you connect a sensor, assuming that it is autodetected and that it implements the ```msensor``` class, it will show up in ```/sys/class/msensor```. See the [individual sensor documentation](Using-Sensors#wiki-list-of-sensors) to find out if a sensor works with the ```msensor``` class.

Sensors are listed by the port that they are connected to.

TODO: To be continued...
