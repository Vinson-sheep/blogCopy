---
title: Ubuntu14mysq5.7不支持中文问题
date: 2017-10-25 20:48:51
categories: "后端"
tags:
     - mysql
description: no
---

> 不得不说，用mysql坑很多，首先就是编码问题。按照网上搜到的答案来处理，很多次我都不能restart mysql了。最后发现是版本问题，在这里我得做文章记录一下。
<!--more-->

mysql本身是不支持中文的，这个我在win10搭建的服务器也碰到过。想要mysql支持中文，就需要更改它的设置。

*请看完这篇文章再动手*

*mysql5.7 Ubuntu14.05*

首先停下mysql服务：
```
sudo /etc/init.d/mysql stop
```
然后用gedit打开mysql配置文件
```
sudo gedit /etc/mysql/my.cnf
```
[client]下添加：
```
default-character-set=utf8
```
[mysqld]下添加：
```
default-character-set=utf8
```
保存退出

重启mysql服务
```
sudo service mysql restart
```
然而...
```
Job failed to start
```

问题在哪呢？
> 可能是版本的问题，查5.5以后的版本对字符编码方式修改的办法，发现[mysqld]修改方法变了：

[mysqld]下添加的应该为：
```
character-set-server=utf8

collation-server=utf8_general_ci
```
保存退出
```
sudo service mysql restart
```
成功

查看字符集
```
mysql> show variables like '%char%';
+--------------------------+----------------------------+
| Variable_name            | Value                      |
+--------------------------+----------------------------+
| character_set_client     | utf8                       |
| character_set_connection | utf8                       |
| character_set_database   | utf8                       |
| character_set_filesystem | binary                     |
| character_set_results    | utf8                       |
| character_set_server     | utf8                       |
| character_set_system     | utf8                       |
| character_sets_dir       | /usr/share/mysql/charsets/ |
+--------------------------+----------------------------+
8 rows in set (0.00 sec)
```

传送们：

[参考资料1——Ubuntu15下mysql5.6.25解决不支持中文的办法](https://www.2cto.com/database/201509/443147.html)

[参考资料2——修改mysql字符编码出现Job failed to start解决办法](https://www.2cto.com/database/201207/139548.html)

[参考资料3——Ubuntu MySQL插入中文出错](http://www.linuxidc.com/Linux/2009-05/20163.htm)
