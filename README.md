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
 
 #!/bin/bash
say() { local IFS=+;/usr/bin/mplayer -ao alsa -really-quiet -noconsolecontrols "https://translate.google.com/translate_tts?ie=UTF-8&client=tw-ob&q=$*&tl=en"; }
say $*
 
 
 ## 6 git the file promission
 
 sudo chmod u+x speech.sh
 
 or more promission:
 
 sudo chmod 777 speech.sh
 
 ## 7 now you can test the reroult
 

 ./speechsh Hello world
 
 
 ./speech.sh hello
 ls -la
 sudo chmod 777 speech.sh
 ./speech.sh hello
