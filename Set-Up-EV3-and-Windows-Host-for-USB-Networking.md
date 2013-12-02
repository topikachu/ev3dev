The modules supplied with the ev3dev kernel allow the EV3 to communicate with host computers using a variety of modes including:

- Serial, using special debug interface that plugs into Sensor Port 1
- WiFi, using a USB dongle

However, these modes require special hardware in the case of a serial driver, or some trial and error getting the WiFi set up correctly. There is, however another communication method that gets us a fast connection with the benefits of standard Ethernet networking such as NFS file shares and ssh access.

On Windows, that means RNDIS networking, and it's actually pretty easy to set up.

![DeviceManager](tree/master/images/WindowsRNDIS/DeviceManager.png)

Adding pictures here for now, add text later
