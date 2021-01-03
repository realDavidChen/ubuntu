
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

$ sudo su

$ whoami

root

$ free -m


$ cat /proc/swaps


$ grep Swap /proc/meminfo

> if you have not swap or no enough swap space, maybe you need to reinstall your Ubuntu(linux) system.
If you have reserve enough swap space, good job! keep move on to next step! 

### Install pm-utils and hibernate:

$ sudo apt install pm-utils hibernate


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

GRUB_CMDLINE_LINUX_DEFAULT="quiet splash resume=UUID=*---YOUR_UUID_VALUE---"

### Then, after saving the file and quitting the text editor, run:

$ sudo update-grub

$ sudo nano /etc/initramfs-tools/conf.d/resume


```
RESUME=UUID=---YOUR_UUID_VALUE---

```

### Re-enable hibernate menu. update the policy kit

$ sudo nano /etc/polkit-1/localauthority/50-local.d/com.ubuntu.enable-hibernate.pkla

 Copy and paste the following value and save the file

```

[Re-enable hibernate by default in upower]
Identity=unix-user:*
Action=org.freedesktop.upower.hibernate
ResultActive=yes

[Re-enable hibernate by default in logind]
Identity=unix-user:*
Action=org.freedesktop.login1.hibernate;org.freedesktop.login1.handle-hibernate-key;org.freedesktop.login1;org.freedesktop.login1.hibernate-m$
ResultActive=yes

```

### To test it, run:

$ sudo systemctl hibernate

### Now restart your computer. next time. then you log out your computer , you can see the "hibernate" and "hybrid sleep" optoin on the list. You can choose one of the options.(note: in my  expreience, sometime I select hibernate ,it can't been wake, if you have same issue.  you can try "hybrid sleep" mode) 
