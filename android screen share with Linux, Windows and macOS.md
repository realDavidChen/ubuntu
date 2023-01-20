# use scrcpy share android to linux(ubuntu) macOS and Windows

https://github.com/Genymobile/scrcpy
https://www.youtube.com/watch?v=Y2rLKsAbngg

## install scrcpy

1. install adb
$ sudo apt install adb

2. linux
$ apt install scrcpy
macOS
$ brew install scrcpy

3. run
$ scrcpy

## connect TCP/IP (wireless)

### method 1

Go to android phone >> Settings >> Wireless & networks/WLAN, or Settings >> Network & Internet >> Wi-Fi >> Network detail >> IP address.

$ adb tcpip 5555
$ adb connect you-are-android-ip-address:5555  // if connected success, return : connected to 192.168.100.50:5555
$ scrcpy 


### method 2
or
$ scrcpy --tcpip    # without arguments

### method 3
connect with ip
$ scrcpy --tcpip=your-android-phone-ip  // default tcpip 5555
or
$ scrcpy --tcpip=your-android-phone-ip:5555



