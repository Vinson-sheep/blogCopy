---
title: Javascript中数字进制的转换
date: 2017-09-30 00:05:44
categories: "前端"
tags:
     - javascript
description: 
---

> 看犀牛书的时候，看到了一些数值转换的方法，再次记录一下。
<!--more-->

javascript中的数值转换利用的是全局函数parseInt()和包装对象方法toString()。

## parseInt()
`parseInt()`可以将任意字符串转换成十进制整数，前提是字符串符合要求。
```
parseInt("3 blind mice")    // => 3
```
对于以`0x`开头的字符串，函数会自动解析为十六进制字符串
```
parseInt("0xFF")    // => 255
parseInt("0xff")    // => 255
```
也可以接受第二个可选参数，用来指定数字转换的基数
```
parseInt("077", 8)  // => 63 (7*8 + 8)
```
> 在ECMAScript 3中，parseInt()是可以对以前缀"0"开头的的数字进行八进制的转换，到了ECMAScript 5之后就被禁止了。如果需要做八进制的转换，需要显式设置。

## s.toString()
先随便定义一个字符串
```
var n = "17";
```
关于这个函数的转换机制就不多说了，直接上实例：
```
var binary_string = n.toString(2)   // 转换为"10001"
var octal_string = "0" + n.toString(8)  // 转换为"021"
var hex_string = "0x" + n.toString(16)  // 转换为"0x11"
```

利用这两个函数，即可在页面上进行随意的数字进制转换。

