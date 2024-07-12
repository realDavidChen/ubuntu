# 在terminal中，实现TTS听代码在线朗读功能

### 安装gtts 和播放器 mpg123

```bash

pip install gtts
sudo apt-get install mpg123

```

写一个python的脚本read_text.py ：

```python
from gtts import gTTS
import os
import subprocess

def read_text(text):
    # 使用 gtts 生成语音文件
    tts = gTTS(text=text, lang='en')
    tts.save("read_text.mp3")

    # 播放生成的语音文件
    os.system("mpg123 read_text.mp3")

if __name__ == "__main__":
    # 运行 man 命令并获取输出
    cmd = "man man"
    output = subprocess.check_output(cmd, shell=True, text=True)

    # 朗读文本
    read_text(output)
```

### 解释：

1. **生成音频文件**：
   ```python
   tts.save("read_text.mp3")
   ```
   这会在当前目录下生成 `read_text.mp3` 文件。

2. **播放音频文件**：
   ```python
   os.system("mpg123 read_text.mp3")
   ```
   这会播放当前目录下的 `read_text.mp3` 文件。

3. **调用 `read_text` 函数**：
   ```python
   read_text(output)
   ```
   传递 `man man` 命令的输出给 `read_text` 函数。

现在，这个脚本会在当前目录生成一个名为 `read_text.mp3` 的文件，并且播放它。你可以根据需要运行脚本来朗读不同的 `man` 页面或其他文本内容。

# 简化听tts的流程


## 版本一： 朗读文本，并输出播放器执行状态

为了实现通过 `man man | gtts` 直接在终端中听到 `gtts` 的朗读声音，你可以按照以下步骤进行操作：

### 1. 创建 `gtts` Python 脚本

创建一个名为 `gtts` 的 Python 脚本文件，内容如下：

```python
#!/usr/bin/env python3

import sys
from gtts import gTTS
import os

def main():
    # 从标准输入读取数据
    input_text = sys.stdin.read()

    # 使用 gtts 生成语音文件
    tts = gTTS(text=input_text, lang='en')
    tts.save("/tmp/output.mp3")

    # 播放生成的语音文件
    os.system("mpg123 /tmp/output.mp3")

if __name__ == "__main__":
    main()
```

### 2. 设置脚本的可执行权限

在终端中，使用以下命令设置脚本的可执行权限：

```bash
chmod +x gtts
```

### 3. 将脚本移动到系统路径

将脚本移动到 `/usr/local/bin` 目录，这样就可以直接使用 `gtts` 命令：

```bash
sudo mv gtts /usr/local/bin/gtts
```

### 4. 使用脚本朗读内容

现在，你可以通过以下命令直接使用 `gtts` 来朗读 `man man` 的内容：

```bash
man man | gtts
```

### 完整步骤总结

1. 创建 `gtts` 脚本文件并写入以下内容：
   ```bash
   touch gtts
   nano gtts
   ```

   内容如下：
   ```python
   #!/usr/bin/env python3

   import sys
   from gtts import gTTS
   import os

   def main():
       input_text = sys.stdin.read()
       tts = gTTS(text=input_text, lang='en')
       tts.save("/tmp/output.mp3")
       os.system("mpg123 /tmp/output.mp3")

   if __name__ == "__main__":
       main()
   ```

2. 设置脚本的可执行权限：
   ```bash
   chmod +x gtts
   ```

3. 将脚本移动到 `/usr/local/bin` 目录：
   ```bash
   sudo mv gtts /usr/local/bin/gtts
   ```

4. 使用 `gtts` 朗读 `man` 命令的内容：
   ```bash
   man man | gtts
   ```

这样，你就可以通过简单的 `man man | gtts` 命令在终端中听到 `gtts` 朗读的内容了。

## 版本二：朗读文本，并同时输出朗读的文本（要终止朗读，按ctr+c）

把python的文件，修改为：

```python
#!/usr/bin/python3

from gtts import gTTS
import os
import sys

def main():
    input_text = sys.stdin.read().strip()

    # 打印原始文本内容
    print("Original Text, Stop tts reader Ctrl + C:")
    print(input_text)

    # 按照常见标点分割文本
    texts = []
    temp_text = ""
    punctuation = "。.，,！!？?；;"

    for char in input_text:
        if char in punctuation:
            temp_text += char
            texts.append(temp_text.strip())
            temp_text = ""
        else:
            temp_text += char
    if temp_text:
        texts.append(temp_text.strip())

    for text in texts:
        if text:  # 确保文本非空
            lang = 'en' if text.encode().isascii() else 'zh'
            tts = gTTS(text=text.strip(), lang=lang)
            tts.save("/tmp/output.mp3")
            os.system("mpg123 /tmp/output.mp3 >/dev/null 2>&1")

if __name__ == "__main__":
    main()



```
其他的设置方法，请直接参考方法一
用这种方法处理的结果，就可以让terminal直接听到tts的同时，能够看到文本的输出
