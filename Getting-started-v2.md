Major changes are afoot. @dlech is trying out some new things and would like your feedback.

## Introduction

By the time you get to this page, you probably already know that ev3dev is Debian Linux for the LEGO Mindstorms EV3. If you have more basic questions, check out the [[FAQ|Frequently Asked Questions]].

## Step 1: Get a Micro SD Card

You need a Micro [SD](https://en.wikipedia.org/wiki/Secure_Digital#SD) or [SDHC](https://en.wikipedia.org/wiki/Secure_Digital#SDHC) card. [SDXC](https://en.wikipedia.org/wiki/Secure_Digital#SDXC) is not supported (you might be able to get it to work, but it will operate at reduced capacity and speed).

Also look at the [speed class rating](https://en.wikipedia.org/wiki/Secure_Digital#Speed_class_rating). Class 10 is the fastest, but slower speeds will work just fine. Ultra High Speed (UHS) classes are not supported (again, they should work, but not at the rated speed).

You will also need a host computer with an adapter for the SD card.

## Step 2: Download the Latest ev3dev Disk Image

In the future, this will be available [here](https://github.com/mindboards/ev3dev/releases), however for testing purposes, download the one from [here](https://github.com/dlech/ev3dev/releases).

Select the image that most closely matches the size of your SD card. Due to variance in SD card capacity, we make the images just a little smaller than the rated capacity. For example if you have a 4GB SD card, then choose `ev3dev.3.9GB.img.zip`. 

**NOTE:** If you want a smaller download, you can select the `.xz` file instead of the `.zip` file, however, this requires that you have additional software installed to decompress it (such as [7-Zip](http://www.7-zip.org/) on Windows). Any recent Linux distro probably has `xz` installed already.

## Step 3: Copy the Image on to the SD Card

There are a vast number of ways to do this, so pick the one from the list that sounds the easiest to you:

* **Linux**
    * [[Writing an Image to a SD Card Using Command Line Tools on Linux|Command Line]]
    * [[Writing an Image to a SD Card Using Graphical Interface Tools on Linux Mint|Linux Mint (graphical interface)]]
    * [[Writing an Image to a SD Card Using Graphical Interface Tools on Ubuntu|Ubuntu (graphical interface)]]
* **Mac OS X**
    * [[Writing an Image to a SD Card Using Command Line Tools on Mac OS X|Command Line]]
    * [[Writing an Image to a SD Card Using Graphical Interface Tools on Mac OS X|Mac OS X (graphical interface)]]
* **Windows**
    * [[Writing an Image to a SD Card Using Win32DiskImager on Windows|Win32DiskImager (graphical interface)]]

## Step 4: Enable USB Networking

Once you have flashed your SD Card, you will need to eject it and then plug it back into your host computer so that we can edit a file.

The SD card has 2 partitions, although you will only see the second one on Linux.

## Step 5: Put the SD Card in your EV3 and Power It On

