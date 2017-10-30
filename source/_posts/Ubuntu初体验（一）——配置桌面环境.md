---
title: Ubuntu初体验（一）——配置桌面环境
date: 2017-09-21 23:22:49
categories: "后端"
tags:
     - Linux
     - Ubuntu
description: Ubuntu配置桌面环境
---

阿里云的服务器，如果使用的是Linux系统，一开始只有命令行界面，对于想要好好学习的我简直吓坏了，所以安装一个界面方便使用。不过要注意，安装桌面环境会一定程度上降低服务器的性能，但是对于我这种简单部署就不会有大的阻碍。
<!--more-->

> 由于我以前使用的是国产的deepin，之后使用阿里云Ubuntu的时候简直吓坏了，只有命令行界面。在安装桌面环境的时候也遇到了各种各样的问题，比如说中文乱码问题。
Ubuntu14.05 桌面gnome3.9

## 安装桌面环境

### 升级一下
```
sudo apt-get update
sudo apt-get upgrade
```

### 安装gnome3.9桌面
依次输入以下命令
```
apt-get install x-window-system-core
apt-get install gnome-core
apt-get install gdm
```
输入`startx`进入桌面环境。可以看到桌面重启后会让你输入root的帐号密码，
![gnome界面](http://ohkgqh4gv.bkt.clouddn.com/126SST10FOY3.png)

## 配置中文环境
> 有些桌面界面会配置好中文环境（至少deepin对中文很友好，毕竟是国产的），而一般外国的桌面都是英文的，连中文都打不进去，更不要说修改什么什么东西了。当我用ftp传输文件的时候，中文会变成带数字的方块。

1. 首先查看一下系统的设定。进入gnome的`system setting`，查看`Region Language`，在`Language`一栏，发现一开始并没有Chinese选项。（如果有，设定为Chinese后重启大概完事）
2. 返回终端,执行以下命令
`sudo apt-get install  language-pack-zh-han*`
这样可以安装中文包。
3. 安装完成后重启服务器。
这时候可以在`Language`一栏看到`Chinese`，将`Language`改为`Chinese`，并且把`input Sources`改为`Chinese`。
4. 再次重启服务器。
重启后发现系统很多原本是英文的地方变成了白色矩形。推测是已经将系统语言变成中文，但是系统并没有装载任何中文字体。
5. 安装中文字体
先安装一个字体
```
sudo apt-get install xfonts-wqy #文泉驿-正黑
sudo apt-get install ttf-wqy-zenhei #思源黑体
```
6. 进入到字体目录下/usr/share/fonts/
```
cd /usr/share/fonts/
```
7. 更新字体
```
sudo fc-cache -fv
```

这时候应该能正常显示中文了。
