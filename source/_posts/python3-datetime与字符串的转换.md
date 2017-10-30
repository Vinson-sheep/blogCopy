---
title: python3 datetime与字符串的转换
date: 2017-10-25 22:58:06
categories: "后端"
tags:
     - python3

description:
---

> 写后台脚本的时候遇到了，mysql输出给pymysql的数据类型为datetime，而json不能直接将datetime对象转化为string，所以需要通过显式转换将datetime转换为string。
<!--more-->

## datetime => string
```
import datetime

date=datetime.datetime.now()
str=date.strftime("%Y-%m-%d %H:%M:%S")
str # => '2017-10-25 23:04:32'
```


## string => datetime
```
import time

str = '2012-08-29 19:45:57'
date = time.strptime(str, "%Y-%m-%d %H:%M:%S")
```

**在这里有一点甚是奇怪**
在本地win10上调试，mysql输出的是datetime对象，但是在Ubuntu14上，mysql的datetime输出的东西可以被json化。关于这个差异，博主在写这篇文章的时候，也没能解决。如果有人看到这篇文字，知道原因，可以发邮件给我。

email: 775014077@qq.com

传送门：

[python time 和datetime类型转换，字符串型变量转成日期型变量](http://www.cnblogs.com/finallyliuyu/archive/2012/02/17/2356160.html)

[python datetime与字符串互转](http://blog.sina.com.cn/s/blog_6ffbcfdb01012zga.html)
