---
layout: default
title: pipinstaller - 可直接执行的文件
parent: Python Recipes
grand_parent: Python
---

# pipinstaller - 可直接执行的文件

## 为什么要做可直接执行的文件？

运行一个.py文件，需要在电脑上安装Python。如果项目中依赖了其它package，需要pip install相关的package。虽然可以通过requirements.txt文件简化package的安装，但是还是需要多余的步骤。

通常在一个项目被完成之后，让这个Python项目更方便地被运行，我们可以通过pipinstaller生成一个可执行的文件，然后可以直接运行这一个可执行文件，不依赖Python环境，不依赖dependency，不依赖Python代码。

## 使用pipinstaller

### 生成可执行文件、

```bash
pip install pyinstaller
pyinstaller --onefile your_script.py
```

如果项目中包含多个.py文件，我们只需要提高main入口对应的那个文件，pyinstaller可以自动找到关联的

如果python依赖其它文件，比如一个json的配置文件，我们在项目完成之后会改动这个配置，又不想重新运行pyinstaller，我们可以声明文件，不把它打包进去。把这个json文件放到生成的可执行文件目录下。这里需要注意的是，Mac和Linux，文件中间用:分隔；Windonws用;分隔。

```bash
pyinstaller --onefile --add-data "config.json:." your_script.py
```

在Python代码中，也要写对应的文件读取规则

```python
import os
import sys
import json

def resource_path(relative_path):
    """ Get absolute path to resource, works for dev and for PyInstaller """
    try:
        # PyInstaller creates a temp folder and stores path in _MEIPASS
        base_path = sys._MEIPASS
    except AttributeError:
        base_path = os.path.abspath(".")

    return os.path.join(base_path, relative_path)

# Usage
json_path = resource_path('config.json')
with open(json_path) as f:
    config = json.load(f)
```

### 执行文件

在我的Mac上，直接执行生成的文件会报错。ChatGPT给出的解释，MacOS没有设置默认的Locale，但是内置的Python解释器需要这个Locale的信息。

```bash
[PYI-10362:ERROR] Failed to start embedded python interpreter!
Fatal Python error: config_get_locale_encoding: failed to get the locale encoding: nl_langinfo(CODESET) failed
Python runtime state: preinitialized
```

最简单的解决办法是再写一个.sh文件，内容为

```bash
#!/bin/bash

# Get the directory where the script is located
SCRIPT_DIR="$(cd "$(dirname "$0")" && pwd)"

export LC_ALL=en_US.UTF-8
export LANG=en_US.UTF-8

# Run the executable, relative to the script
"$SCRIPT_DIR/your_script" "$@"
```

然后给这个文件加上执行的权限

```bash
chmod +x xxx.sh
```

这样，我们在这个dist文件夹下面，就可以执行这个sh文件来运行我们的python脚本。

### 更方便地执行文件

如果这个文件需要经常被执行，我们可以使用ln命令，把这个sh文件symlink到bin文件夹下面。这样就可以在全局直接用myapp命令运行这个文件了。

```bash
ln -s ~/projects/myapp/launch.sh /usr/local/bin/myapp
```

如果我们要删除这个symlink，只需要使用rm删除，它不会影响到原来的sh文件。

```bash
rm /usr/local/bin/myapp
```