## Add application to start-up by terminal

### 1. add you want to startup application to ~/.profile

 
 > example, add golang:


```
$ sudo nano ~/.profile

in the file end, add this code:

export PATH="$PATH:/usr/local/go/bin"
```

### 2. open your terminal, type command again and then, type go, work!

```
$ export PATH="$PATH:/usr/local/go/bin"
$ go version

