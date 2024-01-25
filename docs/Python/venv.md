---
layout: default
title: venv
parent: Python
---

# Python项目虚拟环境`venv`

## 为什么要虚拟环境？

Python有很多功能强大的package，避免了我们重复造轮子。经常我们用使用`pip install <package name>`这种方式安装我们所需的第三方package。但是，这种方式安装的package会默认安装到Python的site-packages目录下。机器上所有的Python项目都会共享这个目录下的package。这样就可能出现一个问题：如果两个项目依赖同一个package的不同版本，就会导致项目运行出错。

为了解决这个问题，Python引入了虚拟环境的概念。虚拟环境可以理解为一个独立的Python环境，它有自己的site-packages目录，可以用来安装和运行独立的package。

## 使用虚拟环境

### 创建虚拟环境
创建`.venv`文件夹
```bash
cd <project dir>
$ python3 -m venv .
```

### 激活虚拟环境 

```bash
$ source .venv/bin/activate
```
激活后，命令行前面会多一个`(.venv)`的标志，表示当前环境是一个虚拟环境。

### 安装package
这时候安装的package会在`.venv/lib/python3.x/site-packages`目录下

```bash
$ pip install <package name>
// 运行python代码
```

### 退出虚拟环境

```bash 
$ deactivate
```

### 删除虚拟环境
就是直接删除`.venv`这个文件夹
```bash
$ rm -rf <env name>
```

## 参考 

- [venv --- 创建虚拟环境](https://docs.python.org/zh-cn/3/library/venv.html) 
- [廖雪峰的Python教程](https://www.liaoxuefeng.com/wiki/1016959663602400/1019273143120480)