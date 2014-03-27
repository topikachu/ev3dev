Major changes are afoot. @dlech is trying out some new things and would like your feedback.

## Introduction

By the time you get to this page, you probably already know that ev3dev is Debian Linux for the LEGO Mindstorms EV3. If you have more basic questions, check out the [[FAQ|Frequently Asked Questions]].

## Step 1: Get a Micro SD Card

You need a Micro [SD](https://en.wikipedia.org/wiki/Secure_Digital#SD) or [SDHC](https://en.wikipedia.org/wiki/Secure_Digital#SDHC) card. [SDXC](https://en.wikipedia.org/wiki/Secure_Digital#SDXC) is not supported (you might be able to get it to work, but it will operate at reduced capacity and speed).

Also look at the [speed class rating](https://en.wikipedia.org/wiki/Secure_Digital#Speed_class_rating). Class 10 is the fastest, but slower speeds will work just fine. Ultra High Speed (UHS) classes are not supported (again, they should work, but not at the rated speed).

You will also need a host computer with an adapter for the SD card.

## Step 2: Download the Latest ev3dev Disk Image

In the future, this will be available [here](https://github.com/mindboards/ev3dev/releases), however for testing purposes, download the one from [here](https://github.com/dlech/ev3dev/releases).

Select the image that most closely matches the size of your SD card. Due to variance in SD card capacity, we make the images just a little smaller than the rated capacity. For example if you have a 4GB SD card, then choose `ev3dev.3900MB.img.zip`. 

**NOTE:** Downloading the `.zip` file is recommended for Windows/Mac and the `.xz` file is recommended for Linux. `.xz` requires that you have additional software installed on Windows/Mac to decompress it (such as [7-Zip](http://www.7-zip.org/) on Windows).

## Step 3: Copy the Image on to the SD Card

**IMPORTANT:** THIS WILL ERASE EVERYTHING ON YOUR SD CARD! BACKUP YOUR FILES IF YOU DO NOT WANT TO LOOSE THEM!

There are a vast number of ways to do this, so pick the one from the list that sounds the easiest to you:

* **Linux**
    * [[Command Line|Writing an ev3dev Image to SD Using Command Line Tools on Linux]]
    * [[Ubuntu (graphical interface)|Writing an ev3dev Image file to SD Using Graphical Interface Tools on Ubuntu]]
* **Mac OS X**
    * [[Command Line|Writing the ev3dev Image to SD Using Command Line Tools on Mac OS X]]
* **Windows**
    * [[Win32DiskImager (graphical interface)|Writing an Image to a SD Card Using Win32DiskImager on Windows]]

**TIP:** If you have partitioning software that can handle resizing ext3 partitions (such as gparted on Linux), you can reclaim the last few MB of your SD card by resizing the ext3 partition.

**TIP:** For more detailed information and more alternatives, check out [this page for RaspberryPi](http://elinux.org/RPi_Easy_SD_Card_Setup). Most of the information there is applicable to ev3dev.

## Step 4: Enable USB Networking

In order to communicate with the EV3, we need a network connection. We are going to setup a TCP/IP connection over USB since USB is the one type of connection that **everyone** has. If you want to use a WiFi dongle or some other type of connection, will will get to that, but we need to set up USB first.

You should still have your SD card plugged in to your host computer. In your file browser/manager/finder/whaterver-you-call-it, there should be a removeable drive called EV3_BOOT. Open it.

There is a file called `ev3dev.rc.local`. Open it in a text editor. **IMPORTANT**: Windows users - do not use Notepad. It will change the line endings and corrupt the file. Use Wordpad or a 3rd party editor such as Notepad++.

Follow the instructions in the file. Uncomment means "delete the `#` at the front of the line.

Windows users should have:

    export EV3_GADGET="g_ether"
    ...
    #export EV3_GADGET="g_cdc"

And Linux/Mac users should have:

    #export EV3_GADGET="g_ether"
    ...
    export EV3_GADGET="g_cdc"

Save and close the file when you are done.

## Step 5: Boot ev3dev

Be sure to safely eject your SD card from you host computer first, then put the SD Card in your EV3 and power it on.

At first, you will see the mindstorms boot splash and the red LEDs will be on. This is immediatly followed by the ev3dev boot splash and the LEDs changing to amber. The left LED indicates CPU activity and the right LED indicates disk (SD card) activity.

Shortly after the ev3dev boot splash, the screen will go blank and then evenually say `"Debian GNU/Linux 7 (wheezy)"`. After the screen goes blank, you can press any of the buttons - except the middle one - to toggle the sysv init messages.

The first boot will take a little longer that subsequent boots because the EV3 has to create a unique SSH host ID.

When the boot is complete, the LEDs will turn green and you will see this on the screen:

                 _____     _
       _____   _|___ /  __| | _____   __
      / _ \ \ / / |_ \ / _` |/ _ \ \ / /
     |  __/\ V / ___) | (_| |  __/\ V /
      \___| \_/ |____/ \__,_|\___| \_/
    
    Debian #OSNAME# 7 on LEGO MINDSTORMS EV3!
    ev3dev tty1
    ev3dev login: _

## Step 6: Use SSH to connect over the USB network interface

This depends on the OS of your host computer, so choose the one that applies:

* Linux
* [[Mac OS X|Connecting via USB on Mac OS X]]
* Windows