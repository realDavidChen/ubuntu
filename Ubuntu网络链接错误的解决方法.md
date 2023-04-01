

## Ubuntu22.04 官方默认的配置网络文件，如果网络无法链接，修改此文件就可以得到解决

### 一. 在 Ubuntu 中配置动态 IP 地址

要从 DHCP 服务器获取 IP 地址，请使用与上述配置文件相同的语法。但不要添加 IP 地址、网关和 DNS 服务器信息。

在这里您可以看到我的动态 IP 寻址配置文件：

#### 编辑文件 
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
#### 测试网络
$ sudo netplan try
如果没有问题，它将返回配置接受消息。 如果配置文件未通过测试，它将恢复为以前的工作配置
#### 应用配置
$ sudo netplan -d apply

#### 重启网络服务
成功应用所有配置后，通过运行以下命令重新启动网络管理器服务：

$ sudo systemctl restart network-manager
#### 如果您使用的是 Ubuntu 服务器，请改用以下命令：

$sudo systemctl restart system-networkd
#### 验证 IP 地址
现在要验证新配置是否成功应用，请运行以下命令来验证 IP 地址：

$ ip a
无论您拥有 Ubuntu 服务器还是台式机，您都可以简单地使用 Netplan 配置静态或动态 IP 寻址，而无需任何复杂的配置。





### 二.在 Ubuntu 中配置静态 IP 地址
要手动配置 IP 地址，请使用上述配置文件语法并添加 IP 地址、网关和 DNS 服务器信息。在这里您可以看到我的静态 IP 寻址配置文件：

```

# Let NetworkManager manage all devices on this system
network:
  version: 2
  renderer: NetworkManager
  ethernets:
    ens33:
      dhcp4: no
      addresses: [192.168.72.150/24]
      gateway4: 192.168.72.2
      nameservers:
        addresses: [8.8.8.8,8.8.4.4]

```

### 

===================
### 此处说明

DEVICE_NAME：接口的名称。

dhcp4：是或否取决于动态或静态 IP 寻址

addresses：设备的 IP 地址以前缀表示法。不要使用网络掩码。

gateway：连接到外部网络的网关 IP 地址

nameservers : DNS 名称服务器的地址

#### 请注意，Yaml 文件的缩进相当严格。使用空格来缩进，而不是制表符。否则，您将遇到错误。

=========================

