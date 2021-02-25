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


