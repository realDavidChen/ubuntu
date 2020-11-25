
# setting Ubuntu 20.04 hibernate

### first and first, Then you install your Uuntu system, you have to   reserve enough swap space

- RAM Size	Swap Size (Without Hibernation)	 Swap size (With Hibernation)
  - 256MB	| 256MB	| 512MB
  - 512MB	| 512MB	| 1GB
  - 1GB	 1GB	 2GB
  - 2GB	 1GB	 3GB
  - 3GB	 2GB	 5GB
 4GB	 2GB	 6GB
 6GB	 2GB	 8GB
 8GB	 3GB	 11GB
 12GB	 3GB	 15GB
 16GB	 4GB	 20GB
 24GB	 5GB	 29GB
 32GB	 6GB	 38GB
 64GB	 8GB	 72GB
 128GB	 11GB	 139GB

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


