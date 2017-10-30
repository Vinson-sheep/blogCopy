---
title: Javascript中instanceof运算符
date: 2017-10-01 00:11:22
categories: "前端"
tags:
     - javascript
description:
---

> 了解javascript中instanceof运算符原理，有利于在实际开发中更好地使用这个运算符。
<!--more-->

## instanceof运算符实例
`instanceof`运算符希望左操作数是一个对象，右操作数标识对象的类。如果左侧的对象是右侧类的实例，则表达式返回true；否则返回false。
```
var d = new Date(); // 创建一个Date对象
d instanceof Date;  // => true
d instanceof Object;  // => false
d instanceof Number;  // => false

var a = [1,2,3];
a instanceof Array;   // => true
a instanceof Object;  // => true
a instanceof RegExp;  // => false
```

## instanceof运算符原理
为了理解`instanceof`运算符是如何工作的，必须首先理解“原型链”。为了计算表达式`o instanceof f`，Javascript首先计算`f.prototype`，然后在原型链中查找`o`，如果找到，返回`true`，否则为`false`。
