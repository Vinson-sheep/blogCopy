---
title: Ubuntu14.05彻底卸载mysql
date: 2017-10-25 22:31:20
categories: "后端"
tags:
     - mysql
     - Ubuntu
     - 转载
description:
---

> 我弄mysql的时候把mysql服务停了，发现有些依赖mysql的功能在Mysql服务重启之后就出了点问题。折腾了许久，愤怒之下决定删mysql再重装，可是我发现mysql卸载一点都不容易。特地写下blog,方便以后使用。
<!--more-->

参考了许多文章，只有这一篇可行。（略有改动）

*mysql5.7 Ubuntu14*

## 停止mysql服务
```
sudo /etc/init.d/mysql stop
```
## 删除mysql的数据文件
```
sudo rm /var/lib/mysql/ -R
```
## 删除mysql的配置文件
```
sudo rm /etc/mysql/ -R
```
## 自动卸载mysql（包括server和client）
```
sudo apt-get autoremove mysql* --purge
sudo apt-get remove apparmor
```
## 检查是否卸载干净
```
dpkg -l | grep mysql # 若没有返回，说明已完成卸载
```
## 接下来安装就是件简单的事情啦
```
sudo apt-get install mysql-server mysql-client
```
这样默认安装的是mysql 5.5的版本，后续尝试安装mysql5.7，稍后补充5.7的安装。


传送门：

[mysql-ubuntu14.04彻底卸载mysql](http://blog.csdn.net/qq_25730711/article/details/53503959)
