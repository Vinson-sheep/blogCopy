---
title: git入门——安装
date: 2017-09-24 21:51:38
categories: "网站维护"
tags:
     - git
     - github
description:
---

> 如果有很多台电脑，每次都要看看找找教程再安装太麻烦了，干脆在这里写好然后多看看。
<!--more-->

## 安装
### windows上面的安装
[下载安装 git for windows](https://git-for-windows.github.io/)
### Ubuntu上面的安装
```
$ sudo apt-get install git
```
### git的设置
因为Git是分布式版本管理系统，所以，每台机器必须自报家门
```
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
```

## 创建版本库
### 创建库文件夹
在一个合适的地方创建文件夹
```
$ mkdir learngit
$ cd learngit
```

### 初始化文件夹
```
$ git init
```
这时候会创建一个名为`.git`的文件夹。

### 远程仓库
#### 创建SSH KEY
```
$ ssh-keygen -t rsa -C "youremail@example.com"
```
这时候会在主目录下找到`.ssh`目录，里面有`id_rsa`和`id_rsa.pub`两个文件，这两个就是SSH Key的秘钥对，id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥，可以放心地告诉任何人。

#### Add SSH KEY
登录GitHub，打开“Account settings”，“SSH Keys”页面：
然后，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴id_rsa.pub文件的内容。

### 远程推送
在本地仓库下执行
```
$ git remote add origin git@github.com:michaelliao/learngit.git
```
然后将本地的所有内容都推送到远程库上
```
git push -u origin master
```
在以后，只要在本地作业，就能通过命令推送到github
```
git push origin master
```

### 克隆库
```
git clone
```
