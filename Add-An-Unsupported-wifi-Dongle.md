## How To Do It

In many cases, you can just plug in your USB wifi dongle and it will "Just Work (tm)" - but sometimes, it just won't. Here's how to get that off brand dongle you bough on DealExtreme to work.

### Figure out the USB pid/vid

Use the 'lsusb' command to dump the current USB device list. For my TPLINK TL-WN725N device, it looks like this:

'''
Bus 001 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
Bus 001 Device 005: ID 0bda:8179 Realtek Semiconductor Corp.
'''

So, good news, the TL-WN725N uses a Realtek chipset, but which one?

### Figure out the chipset details

Head on over to the [Wikidevi site](http://wikidevi.com/wiki/Main_Page), then paste `0bda:8179` into the search window and you'll get some hits for that pid/vid combination.

A bit of reading and you'll find that it uses the Realtek RTL8188EUS chipset - and you can get drivers for it, but only for the Raspberry Pi.

### Wait for someone to build the kernel module

Yeah, this is where you wait for me to build the module from [Larry Finger's rtl8188eu repo](https://github.com/lwfinger/rtl8188eu.git).


