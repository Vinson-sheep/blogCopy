---
title: windows中python读取路径的使用
date: 2017-10-26 23:40:14
categories: "后端"
tags:
     - python3
description:
---

> 由于我是主攻前端的，一般的页面开发会在windons系统上。然而有不得不写后端的时候，比如前端需要api进行调试。我实际学习的时候，我发现python读取文件在Linux和windows的行为不一样。
<!--more-->

首先，"/"左倾斜是正斜杠,"\"右倾斜是反斜杠,可以记为：除号是正斜杠一般来说对于目录分隔符，Unix和Web用正斜杠/，Windows用反斜杠，但是现在Windows

## 目录中的斜杠们
python读文件需要输入的目录参数，列出以下例子：
```
path = r"C:\Windows\temp\readme.txt"
path1 = r"c:\windows\temp\readme.txt"
path2 = "c:\\windows\\temp\\readme.txt"
path3 = "c:/windows/temp/readme.txt"
```
打开文件函数open()中的参数可以是path也可以是path1、path2、path3。

path："\"为字符串中的特殊字符，加上r后变为原始字符串，则不会对字符串中的"\t"、"\r"进行字符串转义

path1：大小写不影响windows定位到文件

path3：用正斜杠做目录分隔符也可以转到对应目录，并且在python中path3的方式也省去了反斜杠\转义的烦恼

## 正则表达式中的斜杠们
正则表达式匹配反斜杠"\"，为什么是"\\\\"或是 r"\\"呢？

因为在正则表达式中\为特殊符号，为了取消它在正则表达式中的特殊意义需要加一个\就变成了\\，但是问题又来了，\也是字符串中的特殊字符，所以又要分别对两个\取消其特殊意义，即为\\\\。Python中有一个原始字符串操作符，用于那些字符串中出现特殊字符，在原始字符串中，没有转义字符和不能打印的字符。这样就可以取消了\在字符串中的转义功能，即r"\\"。

传送门：

[python 对反斜杠的处理问题](https://zhidao.baidu.com/question/240654949866727964.html)
