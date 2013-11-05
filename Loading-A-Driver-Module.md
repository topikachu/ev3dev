## Introduction

Loading modules is easy, if you have the module file accessible via nfs or already loaded on the SD Card.

During the debugging phase, which is where I am most of the time, I load the modules using the command line, like this: `sudo insmod some/path/to/module`, but you can also do it via the startup scripts in Linux.

For now, we'll just use the manual method here. Note that you'll need shell access, either using [ssh over wifi](https://github.com/mindboards/ev3dev/wiki/Setting-Up-wifi-Networking) or soon we'll have RNDIS which will give us IP networking over USB.

1. Somehow, get the kernel module, the file with `.ko` suffix available on the EV3 filesystem. This might mean removing the SD card and copying it manually, of if you've read the page on [setting up an nfs fileshare](https://github.com/mindboards/ev3dev/wiki/Set-Up-An-nfs-FileShare) you can access it over the network.

2. Create the modules directory on the EV3: `sudo mkdir /lib/modules`

3. Copy the module from the source to the EV3: `sudo cp source/path/todriver.ko /lib/modules/driver.ko`

4. Load the driver manually: `sudo insmod /lib/modules/driver.ko`

5. Unload the driver manually: `sudo rmmod /lib/modules/driver.ko`

Of course `driver.ko` should be replaced with the actual driver name! 

## Where to Find Driver Modules

The [ev3dev repository](https://github.com/mindboards/ev3dev) has a directory named `modules` that has all the currently available driver modules.