---
title: pymysql连接mysql数据库——不支持中文解决
date: 2017-09-21 18:52:28
categories: "后端"
tags:
     - pymysql
     - mysql
     - python
description:
---

> 在mysql的学习中，我用本地的win10搭建了环境。当要将中文字符输入到mysql数据库中，就会报错。上网找了一下方法，完美解决。
mysql5.7 windows10

往数据库里插入中文时出现异常:
```
UnicodeEncodeError: 'latin-1' codec can't encode characters
```
就是编码的问题,pymysql默认的编码是latin1,我们只需要把它改成utf8就好了

## 更改pymysql配置文件
1. 打开Python的安装目录:
`Python34\Lib\site-packages\PyMySQL-0.7.9-py3.4.egg\pymysql`
2. 用记事本打开connections.py文件,找到里面的DEFAULT_CHARSET,后面默认=’latin1’,改成utf8就好了,**注意是utf8不是utf-8**。

PS：ubuntu中的路径为：`usr/local/lib/python3.4/dist-packages/pymysql/connections.py`

然而解决了问题了吗？并没有，就算我把connections.py文件所有的latin-1更改为utf8，运行py文件读写数据库依然报错。

于是有了下面的方法：

## 数据库连接
```
db = pymysql.connect('localhost', username, password, database)
```
改为
```
db = pymysql.connect('localhost', username, password, database,use_unicode=True, charset="utf8")
```
解决

[参考资料——博客园](http://www.cnblogs.com/shootercheng/p/5836657.html)
