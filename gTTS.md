## install gTTS and usage

$ sudo -H pip3 install gTTS

usage

$ gtts-cli 'hello' --output hello.mp3

get help 

$ gtts-cli -h


#### note: disable # DefaultModule espeak-ng

$ sudo nano /etc/speech-dispatcher/speechd.conf 

``` 
# DefaultModule espeak-ng 
```

> official website https://gtts.readthedocs.io/en/latest/index.html


