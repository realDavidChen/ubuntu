## install gTTS and usage

$ sudo -H pip3 install gTTS

usage

$ gtts-cli 'hello' --output hello.mp3

get help 

$ gtts-cli -h

> official website https://gtts.readthedocs.io/en/latest/index.html


============
============

##  more method for try:

$  sudo apt install festival speech-dispatcher-festival festvox-{rablpc16k,kallpc16k,kdlpc16k} sox


festvox-{rablpc16k,kallpc16k,kdlpc16k} are voice languages for english
sox, without it only some part of the text where read


## Edit config


$ sudo vim /etc/speech-dispatcher/speechd.conf

Disable espeak-related config and enable festival one

#AddModule "espeak-ng"    "sd_espeak-ng" "espeak-ng.conf"
AddModule "festival"     "sd_festival"  "festival.conf"

#DefaultModule espeak-ng
DefaultModule festival

## Start festival server

Without it I got only some syntences.

$ /usr/bin/festival --server

## Restart Firefox
Then go to reader view mode and try it.
