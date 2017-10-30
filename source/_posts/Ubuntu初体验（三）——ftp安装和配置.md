---
title: Ubuntu初体验（三）——ftp安装和配置
date: 2017-09-22 00:19:03
categories: "后端"
tags:
     - Linux
     - Ubuntu
description:
---

一般编辑文件都会在本地，服务器负责提供服务的。我将系统文件准备好，然后通过ftp推送给Ubuntu，过程很快而且很简单。
<!--more-->

>文章大部分来自百度经验帖（文末），图片同样来自百度经验帖。由于按照百度经验操作会有一些坑，所以就自己写一篇更完整的博客。
win10 + 阿里云 Ubuntu 14.05

## **安装一个基本的文本编辑器（gedit）**
```
sudo apt-get install gedit #安装
sudo apt-get remove gedit #卸载
```


## **Ubuntu中ftp的安装**
### 更新源列表
```
sudo apt-get update
```
![](http://ohkgqh4gv.bkt.clouddn.com/1506013104%281%29.png)
### 安装vsftpd
```
sudo apt-get install vsftpd
```
![](http://ohkgqh4gv.bkt.clouddn.com/1.png)
### 判断vsftpd是否安装成功
```
sudo service vsftpd restart
```
![](http://ohkgqh4gv.bkt.clouddn.com/2.png)
### 新建用户主目录
```
sudo mkdir /home/uftp
```
![](http://ohkgqh4gv.bkt.clouddn.com/3.png)
### 查看是否成功。显示/home下所有可见文件夹。
```
sudo ls /home
```
![](http://ohkgqh4gv.bkt.clouddn.com/4.png)
### 新建用户uftp并设置密码。
```
sudo useradd -d /home/uftp -s /bin/bash uftp #新建用户名uftp
sudo passwd uftp #依次输入两次密码即可
```
![](http://ohkgqh4gv.bkt.clouddn.com/5.png)
### 使用gedit修改配置文件/etc/vsftpd.conf
```
sudo gedit /etc/vsftpd.conf
```
向文件中添加添加
```
userlist_deny=NO
userlist_enable=YES
userlist_file=/etc/allowed_users

seccomp_sandbox=NO
```
![](http://ohkgqh4gv.bkt.clouddn.com/6.png)
![](http://ohkgqh4gv.bkt.clouddn.com/7.png)
同时修改
```
local_enable=YES
```
![](http://ohkgqh4gv.bkt.clouddn.com/8.png)
保存
### 使用gedit新建/etc/allowed_users文件
打开"终端窗口"，输入
```
sudo gedit /etc/allowed_users
```
输入uftp-->保存
![](http://ohkgqh4gv.bkt.clouddn.com/9.png)
### 使用gedit查看/etc/ftpusers文件中的内容
```
sudo gedit /etc/ftpusers
```
打开这个文件后，看一看有没有uftp这个用户名，如果没有，就直接退出。如果有就删除uftp,因为这个文件中记录的是不能访问FTP服务器的用户清单。
![](http://ohkgqh4gv.bkt.clouddn.com/10.png)

## **win端的配置**
### 使用winscp登录FTP服务器
除了winscp之外，还有很多优秀的ftp传输软件，如FileZilla,Xftp等。

下载安装WinSCP，运行WinSCP-->输入IP、用户名、密码-->保存-->勾选"保存密码"-->确定-->登录-->登录成功
![](http://ohkgqh4gv.bkt.clouddn.com/11.png)
### 如果上传失败(大坑)
返回服务器终端
```
chmod -R 777 /home/uftp
```
修改配置文件
```
sudo gedit /etc/vsftpd.conf
```
添加
```
local_root=/home/uftp
write_enable=YES
```
重启vsftpd服务
```
service vsftpd restart
```


[参考资料——百度经验](http://jingyan.baidu.com/article/67508eb4d6c4fd9ccb1ce470.html)
[参考资料——550 Permission denied](http://blog.csdn.net/zilong10_24/article/details/51030265)
[参考资料——553 Could not create file](http://blog.csdn.net/wengyupeng/article/details/44938189)
