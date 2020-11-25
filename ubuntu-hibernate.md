
# setting Ubuntu 20.04 hibernate

### Assume you have a swap partition ready to use.

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

### Right now no GNOME extension is working to have the hibernate option back in the system menu.


