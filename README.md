#google text to speech(TTS) on Linux(Ubuntu)
## 1. app update

sudo apt update 

## 2.install alsa-utils

sudo apt-get install alsa-utils

## 3.edit file 

sudo nano /etc/modules

in the file end, add:

snd_bcm2835

## 4.install mplayer audio and settings

sudo apt install mplayer -y
.....

### setting:
sudo nano /etc/mplayer/mplayer.conf
in the end to add line:
nolirc=yes

## 5 create file: speech.sh
 
 sudo nano speech.sh
 
 
 
 
 sudo chmod u+x speech.sh
 ls
 ./speechsh Look David
 ./speech.sh hello
 ls -la
 sudo chmod 777 speech.sh
 ./speech.sh hello
