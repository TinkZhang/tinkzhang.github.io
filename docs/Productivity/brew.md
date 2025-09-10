---
layout: default
title: 使用homebrew管理Mac软件
parent: Productivity
---

# 为什么要用homebrew

我以前是这样管理Mac上的软件的：

* 下载：想要下载某个软件，一般是Google到它的官网，然后在官网上下载对应的dmg文件，下载完成后点击安装。对于Mac，只需要把软件拖到Application文件夹下面。最后把dmg文件扔进垃圾箱删除掉。

* 更新：打开对应的软件，点击软件的更新检查，触发内置的更新流程，重启一下软件，完成更新。

* 删除：把软件从Application文件夹下拖到垃圾箱，或者右键点删除。

* 备份：？？把软件的安装文件放在某个特定文件夹下面，下次重装电脑或者设置新电脑时掏出来用。

最近公司的Mac遇到了一些问题，需要整个电脑重装一下。平时我的所有数据都在Documents文件夹下面，打个包存在U盘，重装完成之后挪回来就可以了。但是工作电脑上装了不少的软件，我就需要先记录下所有需要的软件，然后在系统重装完成后，把它们一个一个安装回来。回想过去，每次入职新公司或者满3年公司换新电脑，都需要走这么一遍流程，应该有成熟的解决方案，而这个解决方案就是很多Mac用户已经安装的Homebrew。只不过大家经常只是用它来安装软件，没有利用它管理软件。

# 如何使用homebrew

## 安装homebrew

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

## 安装单个软件

```bash
brew install --cask "google-chrome"
```

## 安装多个软件

```bash
# 根目录创建Brewfile
cd ~
vi Brewfile
# 编辑 Brewfile
# 如 cask "notion"
#    cask "firefox"


# 安装所有软件
brew bundle
```

## 备份当前安装的软件

```bash
brew bundle dump  
```

## 更新安装的软件

```bash
# 更新所有软件
brew update && brew upgrade && brew cleanup

# 查看哪些软件可以更新
brew outdated

# 查看哪些 Cask 应用可以更新  
brew outdated --cask     
```

# 优点和局限

优点很明显，只要周期性地备份Brewfile这个文件，我们就能获得Mac上安装的软件列表，并且在需要的时候，可以很快地在新电脑上安装它们。

通过这种方法的局限，不是所有的软件都能通过homebrew安装，比如ClashX，SuperThread等。所以对于它们，还是需要有个记录的地方，希望这类软件越来越少。


# 2025.09.10 我的软件列表（Brewfile）

```bash
########### Productivity ############
# Raycast
cask "raycast"

# Notion
cask "notion"

# Firefox
cask "firefox"

# Chrome
cask "google-chrome"

# Todoist
cask "todoist-app"

# WeChat
cask "wechat"

# WeCom
cask "wechatwork"

# Zoom
cask "zoom"

# Tencent Meeting
cask "tencent-meeting"

# Tunnelblick
cask "tunnelblick"

# PDF Expert
cask "pdf-expert"

# Xmind
cask "xmind"

# Hidden Bar
cask "hiddenbar"


########## Dev & QA ###########

# UV
brew "uv"

# BeeKeeper Studio
cask "beekeeper-studio"

# Proxyman
cask "proxyman"

# Postman
cask "postman"

# iterm2
cask "iterm2"

# PyCharm
cask "pycharm"

# Android Studio
cask "android-studio"

# VS Code
cask "visual-studio-code"

# Github Desktop
cask "github"

# Cursor
cask "cursor"

# Trae
cask "trae-cn"
```