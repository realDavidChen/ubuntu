Here is the complete backup guide summarizing your keyboard layout adjustments on your Mac Air running Xubuntu.
这是你在 Mac Air 上运行 Xubuntu 的键盘布局调整完整备份指南。

---

## 1. Function Keys Configuration ($F1 - F12$)

## 1. 功能键配置 ($F1 - F12$)

### Goal

### 目标

Make $F1 - F12$ trigger application functions directly, and require $Fn + F1 - F12$ for system adjustments like brightness or volume.
让 $F1 - F12$ 直接触发应用程序功能，而需要按下 $Fn + F1 - F12$ 来调节亮度或音量等系统设置。

### Steps

### 步骤

Open the terminal and edit the Apple keyboard module configuration file:
打开终端并编辑苹果键盘模块配置文件：

`sudo nano /etc/modprobe.d/hid_apple.conf`
`sudo nano /etc/modprobe.d/hid_apple.conf`

Add the following configuration line to the file:
将以下配置行添加到文件中：

`options hid_apple fnmode=2`
`options hid_apple fnmode=2`

Save the file ($Ctrl + O$, then $Enter$) and exit ($Ctrl + X$).
保存文件（$Ctrl + O$ 然后回车）并退出（$Ctrl + X$）。

Update the system ramdisk to apply the configuration during boot:
更新系统内存盘以便在启动时应用配置：

`sudo update-initramfs -u`
`sudo update-initramfs -u`

Restart your computer to complete the configuration.
重新启动电脑以完成配置。

---

## 2. Key Remapping (Command $\leftrightarrow$ Control)

## 2. 键位重映射 (Command $\leftrightarrow$ Control)

### Goal

### 目标

Map both left and right **Command** keys to function as **Control**, and change the original left **Control** key into the **Super/Win** key.
将左侧和右侧的 **Command** 键都映射为 **Control** 键功能，并将原来的左侧 **Control** 键变成 **Super/Win** 键。

### Steps

### 步骤

Install the hardware-level key remapping tool `keyd`:
安装硬件级键位重映射工具 `keyd`：

`sudo apt update && sudo apt install -y keyd`
`sudo apt update && sudo apt install -y keyd`

Create and edit the `keyd` configuration file:
创建并编辑 `keyd` 配置文件：

`sudo nano /etc/keyd/default.conf`
`sudo nano /etc/keyd/default.conf`

Paste the exact mapping rules into the file:
将准确的映射规则粘贴到文件中：

```text
[ids]
*

[main]
leftmeta = leftcontrol
leftcontrol = leftmeta
rightmeta = rightcontrol

```

```text
[ids]
*

[main]
leftmeta = leftcontrol
leftcontrol = leftmeta
rightmeta = rightcontrol

```

Save the file ($Ctrl + O$, then $Enter$) and exit ($Ctrl + X$).
保存文件（$Ctrl + O$ 然后回车）并退出（$Ctrl + X$）。

Enable and restart the background system service to apply the layout immediately:
启用并重启后台系统服务以立即应用该布局：

`sudo systemctl enable keyd && sudo systemctl restart keyd`
`sudo systemctl enable keyd && sudo systemctl restart keyd`

> **Note:** The `source` command is not used here because system directory configurations are loaded directly by background services rather than the shell.
> **注意：** 这里不需要使用 `source` 命令，因为系统目录下的配置文件是由后台服务直接加载的，而不是由 shell 加载。
