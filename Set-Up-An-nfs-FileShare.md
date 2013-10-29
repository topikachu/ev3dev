## Why Do It?

The nfs protocol is the standard Linux way to share files between computers, and since you're running Linux on the EV3, and there's nfs support built-in, you can share files between your computer and the EV3 without having to pull the card all the time.

Using a file share method like nfs makes it easier for folks like me to load and unload modules that are under development. That saves time and is less error prone than swapping SD Cards and rebooting all the time.

For general users, it makes it easy to upgrade their SD Cards with known good modules and other updates to config files. It also makes it easier to backup your SD card. Finally, it allows you to edit code on your host machine, then run it on the EV3 without having to actually copy files anywhere!

_Note to self: Add a picture here so it's clear what's being shared where!_

It's dead easy, all you have to do is modify one file on the EV3 and one on your computer. Let's start with getting the computer set up. 

## How To Do It - Linux

On your Linux box, you'll need to edit a file called `/etc/exports`. If you don't have this file, then you need to install `nfs-common` or a similar package. Update the file to look like this:

````
# /etc/exports: the access control list for filesystems which may be exported
#		to NFS clients.  See exports(5).
#
# Example for NFSv2 and NFSv3:
# /srv/homes       hostname1(rw,sync,no_subtree_check) hostname2(ro,sync,no_subtree_check)
#
# Example for NFSv4:
# /srv/nfs4        gss/krb5i(rw,sync,fsid=0,crossmnt,no_subtree_check)
# /srv/nfs4/homes  gss/krb5i(rw,sync,no_subtree_check)
#

# Share the /home/youruserid/nfs/ev3dev directory on this computer with anyone (*)
# on the local 192.168.254.* network that asks. If your wifi network assigns a
# constant IP address to the EV3, then replace the * with the specific address...
#
/home/youruserid/nfs/ev3dev   192.168.254.*(rw,sync,no_subtree_check,root_squash)
````

There may be more lines, of course. All you need to do is tell nfs which directory
you want to share (`/home/youruserid/nfs/ev3dev`) and who you want to share it with (`192.168.254.*`).

The options, enclosed in parenthesis, tell nfs to:

- Allow read/write access
- Don't process a write request until the previous write is committed to disk
- Disables subtree checks, more reliable but mild security risk
- Do not let root on the EV3 to be like root on the host, good idea!

So update the file on your host machine, then run `sudo exportfs -rv` which will update the directories that nfs exports. On to the EV3..

## How To Do It - Windows/Mac

No clue yet - if someone is kind enough to donate an x86 based Mac, or instructions for setting up nfs shares then I'll be happy to add them here.

## How To Do It - EV3

On the EV3, you'll need to update a file (as root) called `/etc/fstab`. It's much easier to do this either via a serial console, or if you have wifi working, then `ssh` to the EV3 and run an editor like `vi` or `nano` to edit the file. Here's the line you want to add to `/etc/fstab` - DO NOT TOUCH ANYTHING ELSE IN THERE!

```
/dev/mmcblk0p1 /media/mmc_p1 vfat noatime  0 0
/dev/mmcblk0p2 /             ext3 noatime  0 0
proc           /proc         proc defaults 0 0

# Here's the line that says where to find the share, and where to mount it locally!
#
192.168.254.227:/home/youruserid/nfs/ev3dev /home/ev3dev/nfs/ev3dev nfs users,auto,rw,vers=3  0 0
```

It's not too hard to figure out what's going on here. The host machine with the nfs mount is at `192.168.254.227` and we added `/home/youruserid/nfs/ev3dev` to the `/etc/exports` file on that machine. The next section of the line says we want to mount it locally at `/home/ev3dev/nfs/ev3dev` - if you've added a different userid for yourself, instead of the default `ev3dev` then change it.

The options tell `mount` that:

- this is an nfs share
- general users are allowed to mount the share
- we want read/write access
- we are using nfs V3 on the host

Once you've updated the `/etc/fstab` file, all you need to do is mount the share, like this:

`mount ~/nfs/ev3dev`

And then you should be able to see the files on your PC!

## References

The [Linux `exports`](http://linux.die.net/man/5/exports) manpage
The [Linux `exportfs`](http://linux.die.net/man/8/exportfs) manpage