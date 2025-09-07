---
layout: default
title: uv
parent: Python Recipes
grand_parent: Python
---

# Python项目依赖管理工具

## 又一种Python项目依赖管理工具

Python有很多功能强大的package，避免了我们重复造轮子。Python有很多中依赖的管理工具，比如使用`pip install <package name>`这种方式安装我们所需的第三方package。但是，这种方式安装的package会默认安装到Python的site-packages目录下。机器上所有的Python项目都会共享这个目录下的package。这样就可能出现一个问题：如果两个项目依赖同一个package的不同版本，就会导致项目运行出错。而且site-packages会越来越臃肿，会导致各种不易察觉的问题。

为了解决这个问题，Python引入了虚拟环境的概念。虚拟环境可以理解为一个独立的Python环境，它有自己的site-packages目录，可以用来安装和运行独立的package。

过去，我们需要手动创建并且管理这个虚拟环境。`uv`是一个依赖管理器，它的底层还是虚拟环境，但是它提供了一些更简单直观的方法，让我们不用自己管理`.venv`了。

## 0.安装uv

[uv官方安装方法](https://docs.astral.sh/uv/getting-started/installation/)

对于MacOS，可以用brew进行安装

```bash
brew install uv
```

## 1.在单文件Python脚本中使用uv

### 1.0.运行单个Python文件

```bash
uv run main.py
```

Python经常被用来当作脚本语言，一个简单的`.py`文件就能执行一项工作。

### 1.1.运行时指定依赖

```python
# main.py

import sys
import requests # 假设这个脚本需要使用requests这个库

print(sys.version)
print("Hello, World")
```

过去，对于这样有依赖的单文件项目，我也是建立一个项目，然后用`requirements.txt`管理它的依赖，有点杀鸡用牛刀了。uv对于这个场景有几种不同的方式可供我们选择。


使用`--with`参数添加依赖，如果需要多个依赖，就用多个`--with`

```bash
uv run --with requests main.py
uv run --with requests --with flask main.py
```

如果依赖的项目比较多，这种方法就不是很方便。

### 1.2.在文件中定义依赖

先用`init --script`初始化，效果是会在文件头部添加script

```bash
uv init --script main.py
```

```Python
# /// script
# requires-python = ">=3.13"
# dependencies = []
# ///
```

然后我们可以添加依赖

```bash
uv add --script main.py 'requests<3' 'rich'
```

生成的python就会添加dependencies。

```Python
# /// script
# requires-python = ">=3.13"
# dependencies = [
#   "requests<3",
#   "rich",
#]
# ///
```

我们也可以直接编辑python文件头部的script，增加或者删除依赖，效果是一样的。

### 1.3.使用shebang创建可运行文件

为了执行的时候不用输 `uv run --script main.py`，可以在文件最上面加上一行shebang。

```Python
#!/usr/bin/env -S uv run --script
#
# /// script
# requires-python = ">=3.13"
# dependencies = [
#   "requests<3",
#   "rich",
#]
# ///

import sys
import requests # 假设这个脚本需要使用requests这个库

print(sys.version)
print("Hello, World")
```

这样我们给文件运行权限后，将可以直接运行了

```bash
chmod +x main.py
./main.py
```

## 2.在项目中使用uv

### 2.0.创建项目

```bash
uv init hello-world

# 在项目的根目录中
uv init
```

生成的文件有

```bash
.
├── .venv
│   ├── bin
│   ├── lib
│   └── pyvenv.cfg
├── .python-version
├── README.md
├── main.py
├── pyproject.toml
└── uv.lock
```

其中，与依赖管理相关的文件是`pyproject.toml`

```bash
[project]
name = "hello-world"
version = "0.1.0"
description = "Add your description here"
readme = "README.md"
dependencies = []
```

### 2.1.管理依赖

```bash
uv add requests
uv add 'requests==2.31.0
uv add git+https://github.com/psf/requests

# 迁移自requirements.txt
uv add -r requirements.txt -c constraints.txt

# 删除
uv remove requests

# 更新版本
uv lock --upgrade-package requests
```

### 2.2.依赖同步

`uv sync` 会同步.venv 和pyproject.toml。`uv lock` 会生产 uv.lock文件

`uv run`会自动调用sync，sync时会自动调用lock，所以一般我们不需要手动去sync或者lock，除非我们改变了依赖，但是没有run，又需要提交commit

## 参考 

- [uv官方文档](https://docs.astral.sh/uv/) 
- [Stop Using Pip - This New Tool is 100x Faster (UV Tutorial)](https://www.youtube.com/watch?v=6pttmsBSi8M&ab_channel=TechWithTim)