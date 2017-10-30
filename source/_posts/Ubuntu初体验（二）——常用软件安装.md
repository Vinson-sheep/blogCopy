---
title: Ubuntu初体验（二）——常用软件安装
date: 2017-09-22 00:18:29
categories: "后端"
tags:
     - Linux
     - Ubuntu
description: Ubuntu配置桌面环境
---

安装过中文桌面后，还有一些常用的软件需要下载，如winrar等。对于是否安装软件，我的建议是能少就少，有什么从本地ftp推给服务器。
<!--more-->

## 安装搜狗输入法
1. 用自带的浏览器（gnome的是firefox）打开网址
`http://pinyin.sogou.com/linux/?r=pinyin`
2. 下载你需要的输入法版本，我这里是64位版的Ubuntu
3. 下载完成后安装deb文件，跟着提示操作即可。
4. 在终端输入`im-config`。跟着出现的对话框，点击>OK>yes，点击fcixt>OK。
5. 重启服务器，开始使用sogou输入法

[参考文章](http://jingyan.baidu.com/article/ad310e80ae6d971849f49ed3.html)

## 安装文本编辑器(atom为例)
1. 使用PPA下载
```
sudo add-apt-repository ppa:webupd8team/atom
sudo apt-get update
sudo apt-get install atom
```
2. 执行第一条的时候可能会报错
`sudo:add-apt-repository:command not found`
3. 终端运行以下命令后再使用PPA
```
sudo apt-get install python-software-properties
sudo apt-get install software-properties-common
```
4. 如果你想卸载
```
sudo apt-get remove atom
sudo add-apt-repository --remove ppa:webupd8team/atom
```

## WinRAR安装
```
sudo apt-get install rar
sudo ln -fs /usr/bin/rar /usr/bin/unrar
```
