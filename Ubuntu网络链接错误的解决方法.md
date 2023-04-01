

## Ubuntu22.04 官方默认的配置网络文件，如果网络无法链接，修改此文件就可以得到解决

编辑文件 
$ sudo vim /etc/netplan/01-network-manager-all.yaml

把代码粘帖到代码区中

```
# Let NetworkManager manage all devices on this system
network:
  version: 2
  renderer: NetworkManager
  ethernets:
    ens33:
      dhcp4: yes

```

:wq 保存并退出
### 测试网络
$ sudo netplan try
如果没有问题，它将返回配置接受消息。 如果配置文件未通过测试，它将恢复为以前的工作配置
### 应用配置
$ sudo netplan -d apply
