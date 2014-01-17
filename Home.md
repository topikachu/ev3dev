Watch this space for more detailed instructions than those in the individual README.md files in the repository.

Let's get started - every new article gets added to the top of this list - when there's enough we'll start to categorize them.

### Getting Started

- [Writing A microSD Card](wiki/Writing-A-microSD-Card)

The easiest way to get started with `ev3dev` hacking is to use USB/Ethernet networking so that you can `ssh` directly to the brick without the need for a wifi conenction.

We're assuming that you've got:

1. A [microSD card with the `ev3dev` image](wiki/Writing-A-microSD-Card) loaded
2. The USB cable that comes with the EV3
3. A Linux/OSX/Windows host computer/tablet with a free host USB port
4. The `ev3dev.rc.local` file on the FAT32 partition of the microSD card configured for your host machine.

Connect the USB-mini end of the cable to the EV3, and leave the host end disconnected from your computer for now. Then boot the EV3. When you see the `ev3dev` signon logo on the LCD, you know that the EV3 is ready to communicate with your host machine.

- [Setting Up Linux USB Ethernet Networking](wiki/Setting-Up-Linux-USB-Ethernet-Networking)
- [Setting Up Windows Ethernet Networking](wiki/Setting-Up-Windows-USB-Ethernet-Networking)
- [Setting Up OSX Ethernet Networking](wiki/Setting-Up-OSX-USB-Ethernet-Networking)

### Next Steps

- [Setting Up wifi Networking](wiki/Setting-Up-wifi-Networking)
- [Set Up An nfs FileShare](wiki/Set-Up-An-nfs-FileShare)
- [Add An Unsupported wifi Dongle](wiki/Add-An-Unsupported-wifi-Dongle)
- [Loading A Driver Module](wiki/Loading-A-Driver-Module)

### Documentation on Individual Loadable EV3 Drivers

- [Using the ev3dev_ui.ko Module](wiki/Using-the-ev3dev_ui.ko-module)

###Hacking

Want to contribute to the ev3dev kernel? Or just learn more about how things work at a low level? Check out the [Kernel Hackers Notebook](wiki/ev3dev-Kernel-Hackers-Notebook).