
# setting Ubuntu 20.04(or other linux system) hibernate

### Assume you have a swap partition ready to use and have to  reserve enough swap space
### how many swap space enough for hibernate?

> RAM Size	Swap Size (Without Hibernation)	 Swap size (With Hibernation)

- |RAM   |without |hibernation
- |256MB |256MB |512MB
- |512MB |512MB |1GB
- |1GB   |1GB   |2GB
- |2GB   |1GB   |3GB
- |3GB   |2GB   |5GB
- |4GB   |2GB   |6GB
- |6GB   |2GB   |8GB
- |8GB   |3GB   |11GB
- |12GB  |3GB   |15GB
- |16GB  |4GB   |20GB
- |24GB  |5GB   |29GB
- |32GB  |6GB   |38GB
- |64GB  |8GB   |72GB
- |128GB |11GB  |139GB

### check your linux system memory and swap status

$ free -m


$ cat /proc/swaps


$ grep Swap /proc/meminfo

> if you have not swap or no enough swap space, maybe you need to reinstall your Ubuntu(linux) system.
If you have reserve enough swap space, good job! keep move on to next step! 

### Install pm-utils and hibernate:

sudo apt install pm-utils hibernate


### Then:

$ cat /sys/power/state

You should see:

freeze mem disk
### Then run:

$ grep swap /etc/fstab


UUID=************************************ none

### Copy the UUID value. You will need it later. Then run:

$ sudo nano /etc/default/grub

(or your favourite editor if not nano). Change the line that says

GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"
so that it instead says:

GRUB_CMDLINE_LINUX_DEFAULT="quiet splash resume=UUID=YOUR_VALUE"

### Then, after saving the file and quitting the text editor, run:

$ sudo update-grub

To test it, run:

$ sudo systemctl hibernate

> Right now no GNOME extension is working to have the hibernate option back in the system menu.

## Ubuntu won't recover after hibernate mode

### Step 1: Open up a terminal and create a script file as follows:

$ sudo gedit /etc/pm/sleep.d/20_custom-ehci_hcd

### Step 2: Copy the entire script below into the file you just created and save it:

```#!/bin/sh
#inspired by http://art.ubuntuforums.org/showpost...0&postcount=19
#...and http://thecodecentral.com/2011/01/18...ot-working-bug
# tidied by tqzzaa :)
VERSION=1.1
DEV_LIST=/tmp/usb-dev-list
DRIVERS_DIR=/sys/bus/pci/drivers
DRIVERS="ehci xhci" # ehci_hcd, xhci_hcd
HEX="[[:xdigit:]]"
MAX_BIND_ATTEMPTS=2
BIND_WAIT=0.1
unbindDev() {
echo -n > $DEV_LIST 2>/dev/null
for driver in $DRIVERS; do
DDIR=$DRIVERS_DIR/${driver}_hcd
for dev in `ls $DDIR 2>/dev/null | egrep "^$HEX+:$HEX+:$HEX"`; do
echo -n "$dev" > $DDIR/unbind
echo "$driver $dev" >> $DEV_LIST
done
#for bus in $EHCI_BUSES; do
echo -n $bus > /sys/bus/pci/drivers/ehci_hcd/unbind
# done
done
}
bindDev() {
if [ -s $DEV_LIST ]; then
while read driver dev; do
DDIR=$DRIVERS_DIR/${driver}_hcd
#for bus in $EHCI_BUSES; do
echo -n $bus > /sys/bus/pci/drivers/ehci_hcd/bind
#done
while [ $((MAX_BIND_ATTEMPTS)) -gt 0 ]; do
echo -n "$dev" > $DDIR/bind
if [ ! -L "$DDIR/$dev" ]; then
sleep $BIND_WAIT
else
break
fi
MAX_BIND_ATTEMPTS=$((MAX_BIND_ATTEMPTS-1))
done
done < $DEV_LIST
fi
rm $DEV_LIST 2>/dev/null
chvt 1
chvt 7
}
EHCI_BUSES="0000:00:1a.0 0000:00:1d.0"
case "$1" in
hibernate|suspend)
unbindDev;;
resume|thaw)
bindDev;;
esac
Step 3:
Give the script run permissions by typing:
sudo chmod 755 /etc/pm/sleep.d/20_custom-ehci_hcd

```

> **test again, run:**

$ sudo update-grub

$ sudo systemctl hibernate

good luck!
