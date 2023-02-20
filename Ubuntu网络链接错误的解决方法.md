#Ubuntu网络链接错误解决方法

## 按网络图标，做常规检查，是否配置正常
## 打开命令行工具，手动配置

$ cd /etc
$ ls
$ sudo vim resolv.conf
把里面的网络用配置用#先注释掉
#nameserver 127.0.0.53
#........
添加自己的配置：
nameserver 8.8.8.8
nameserver 8.8.4.4

vim保持并退出 :wq

打开浏览器，输入网站，如果能正常打开，问题解决
