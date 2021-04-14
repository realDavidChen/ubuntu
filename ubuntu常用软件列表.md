## ubuntu常用软件列表


### Slimjet浏览器

轻量级浏览器，低性能的电脑必备，可以和 chrome帐号互通，支持同步应用插件、收藏夹等，可以和chrome混合着用
（注： chromium内核的浏览器，选择32位可以节省不少内存，64位的速度快一点点，可以看网上相关测评）

下载地址 https://www.slimjet.com/en/dlpage.php   

### plank: 浮动常用工具列表： 

$ sudo apt install plank

安装后把它添加到随机启动状态中,安装后，把常用软件拖到plank中，下次要使用的时候，鼠标滑动到窗口下方，自动浮现软件列表，从列表中移除，选中按钮左键不放拖动图标，放手即可移除

### Stacer 优化软件，超级好用

$ sudo apt install stacer

### Nmap，也就是Network Mapper，最早是Linux下的网络扫描和嗅探工具包

$ sudo apt  install nmap


### 用命令行浏览文件夹，加密文件夹也可以以root身份直接访问

$ sudo apt install nautilus

> 基本使用方法  如： nautilus . 打开当前文件夹

### cheese 摄像头软件

sudo apt-get install cheese 

### flameshot 超好用的屏幕截图软件

$ sudo apt install flameshot

为更加有效的截图或者演示，对flameshot做如下配置： 1.在 keyboard==》application shortcut中，把原来默认的截图软件快捷键 "print screen syspg"键释放给flameshot用. 2. 点+号 添加flameshot的软件位置路径 ``` /usr/bin/flameshot gui ```  进入下一步，设置快捷键，按 ``` print screen syspq ``` 键，然后确定。 3. 需要截图时， 按 ``` print screen syspq ``` 开始截图，如果要添加文字，点文字图标，文字默认情况下字体很小，可以滚动鼠标的滚轮调大，右键可以选择颜色，输入中文文字时看不到面板，如果输入完成后，无法的到你要的结果，可以尝试着配合数字选择键123..或者翻页键-+,来实现输入，按 ``` Esc ``` 键退出。


### trans 命令行翻译软件

$ sudo apt-get install -y translate-shell

### calibre 电子书软件 支持格式齐全，特色，阅读风格，背景颜色可以改变，可以语音TTS阅读，窗口，自动阅读并翻页，编辑等

 $ sudo -v && wget -nv -O- https://download.calibre-ebook.com/linux-installer.sh | sudo sh /dev/stdin

### google translate 翻译工具自制

1. 用chrome浏览器打开 https://translate.google.com/
2. 左侧选择 English， 右侧选择Chinese（或者任何自定义互译的语言）
3. 浏览器右上角settings => more tools => create shortcuts => open as window 勾上，这个时候，就已经在你的桌面上生成了一个快捷的应用了
4. 从桌面点击图标，就可以打开简洁的翻译的窗口，你也可以通过系统搜索到 Google translate, 也可以把这个应用拖放到plank托盘，方便打开
5. 也可以给这个应用设置一个快捷键，在系统的 keyboard 里面设置，把路径指向桌面（不是标准的应用，选择查看全部内容，即可显示，并选中，然后设置快捷键）
6. 让软件置顶 alt+空格键  在弹出的选项中，选中 always on top

### epy 用命令行阅读电子书（除了没有图片，其他体验都不错）

https://github.com/realDavidChen/epy

$ pip3 install epy-reader

- 打开电子书的方法：
  - $ ls    
    显示当前目录下的电子书书名
  - $ epy '电子书的书名'
  
  - 如果图书阅读到一半退出，下次再次打开只需要输入 $ epy 就可以
  
  - 快捷键： t 回到目录 箭头键上下选择 enter键确认 在进入图书内容的情况下，点 c 键可以切换背景颜色 箭头方向键换页或空格键翻页  退出epy ctrl+c
- 支持tts阅读的 在打开的内容中，按快捷键 ! 开始朗读，当然，前提是要先安装TTS语音引擎
```  $ apt install libttspico-utils sox ```

跟多的快捷键的方法或配置，请看：
Config file is available in json format which is located at:
```
Linux: cat ~/.config/epy/config.json or cat ~/.epy/config.json
Windows: %USERPROFILE%\.epy\config.json
  
```
本软件还支持tts发音的 


### googler 命令行google搜索

https://github.com/jarun/googler

```install
$ sudo apt update
$ sudo apt install googler
$ googler --version

// get help

$ googler -h

```
### 查看计算机硬件信息

$ sudo apt-get install hardinfo

打开软件直接输入 

$ hardinfo

### viu terminal命令行支持图片 

git clone https://github.com/atanunq/viu.git

From source (recommended)
Installation from source requires a local Rust environment.

```

git clone https://github.com/atanunq/viu.git

# Build & Install
cd viu/
cargo install --path .

# Use
viu img/giphy.gif
```
Or without cloning:
```

cargo install viu

```


**使用方法方法说明**

- $ trans --help 获得帮助文件
- $ trans  # 回车后进入系统默认的语言翻译
- $ trans :zh  # 翻译成中文
- $ trans :zh+en  # 同时翻译成两种语言，可以自己定义
- $ trans :zh -p -b   # 混合设置范例：  :zh 翻译成中文 -p语音播放，-b 简洁模式

**技巧补充**

为了节省时间，不想每次为了按得到自己想要的翻译效果而敲打大量的命令，这里有个非常简单的技巧，就是命令替换

1 设置别名
$ vim ~/.bashrc
2 在vim编译器下,输入i进行编写,找到下面代码,在下面添加即可

$ alias c='trans :zh -b'

说明：上面这段话的意思是用自定义的c键，或者任何你想自定义的快捷键都可以（不要和系统快捷键冲突就可以，输入你要的字母，回车，如果提示命令不存在，即可使用）=替换右侧的 trans 软件名称:zh 翻译成中文 -b简洁模式\
trans的具体用法， 输入 $ trans --help 自己查询
:wq 保存并退出

3 重新载入，让命令马上生效

$ source ~/.bashrc





# 开发软件

==============

netstat 网络端口检测软件

sudo apt install net-tools

$ netstat -nltp


