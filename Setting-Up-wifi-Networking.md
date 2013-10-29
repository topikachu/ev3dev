# How to Do It #

In my original README text for these repos, I mistakenly suggest that it's a good idea to update the /etc/network/interfaces file with your wifi details. That's actually a bad idea. It works if you're only ever connected to one wifi network, but if you want to take your EV3 to school or the office then you'll want a more general solution.

Thanks to [Xander](http://botbench.com/) for setting me straight on the right way to do it!

Edit /etc/network/interfaces to look like this:

> root@ev3dev:~# cat /etc/network/interfaces
> auto lo
> iface lo inet loopback
>  
> auto wlan0
> iface wlan0 inet dhcp
>     wpa-conf /etc/wpa_supplicant.conf

And /etc/wpa-supplicant.conf to look like this:

> root@ev3dev:~# cat /etc/wpa_supplicant.conf
> ctrl_interface=/var/run/wpa_supplicant
> network={
>        ssid="Your SSID Here"
>        scan_ssid=1
>        proto=WPA RSN
>        key_mgmt=WPA-PSK
>        pairwise=CCMP TKIP
>        group=CCMP TKIP
>        psk="Your text key here"
> }

Just add another copy of the "network" section for every new network, and fill int the SSID and psk details.

Of course, that's much easier to do when you can ssh into your EV3 already! It's handy to have your serial interface just in case.

# References #

[Main wpa-supplicant page](http://w1.fi/wpa_supplicant/) - Go to the section on "Configuration File" for samples
