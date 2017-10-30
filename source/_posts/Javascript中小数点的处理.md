---
title: Javascript中小数点的处理
date: 2017-09-30 00:30:12
categories: "前端"
tags:
     - javascript
description: 
---

> 在处理财务或科学数据的时候，在做数字到字符串的转换过程中，你期望自己控制输出中小数点位置和有效数字位数，或者决定是否需要指数计数法。
<!--more-->

Number类为数字到字符串的转换提供三个方法`toFixed()`、`toExponential()`、`toPrecision()`,它们都有一个必须的数值参数。

先定一个数字
```
var n = 123456.789
```
## toFixed 固定的
根据小数点后的指定位数将数字转换为字符串。它从不使用指数记数法
```
n.toFixed(0);   // "123457"
n.toFixed(2);   // "123456.79"
n.toFixed(5);   // "123456.78900"
```
## toExponential 指数的
使用指数记数法将数字转换为指数类型的字符串，其中小数点前只有一位，小数点后的位数则由参数指定
```
n.toExponential(1);     // "1.2e+5"
n.toExponential(3);     // "1.235e+5"
```
## toPrecision 精密的
根据指定的有效数字位数将数字转换成字符串。如果有效数字少于数字整数部分的位数，则转换成指数形式。
```
n.toPrecision(4);   // "1.235e+5"
n.toPrecision(7);   // "123456.8"
n.toPrecision(10);  // "123456.7890"
```

我们注意到，所有三个方法都会适当地进行四舍五入或填充0.

另外，`toExponential`、`toPrecision`的转换都是不可逆，无法通过`toString`变成原始值。



