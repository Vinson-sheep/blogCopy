---
title: Javascript严格模式
date: 2017-10-05 00:15:12
categories: "前端"
tags:
     - javascript
description:
---

> 严格模式修复了JS中的重要缺陷，并提供健壮的差错功能和增强的安全机制。但由于一般不会特别去声明是strict模式，用得比较少，在这里只是做个简介，如果有需要的话，再在本文扩充。
<!--more-->

“use strict”是ECMAScript 5引入的一条指令。指令不是语句（但非常接近语句）。

使用“use strict”指令的目的是说明（脚本或者函数中）后续的代码将会解析为严格代码（strict code）。

对于那些不支持strict模式的浏览器，“use strict”只是一条没有副作用的表达式语句而已，它什么都不做。

严格模式和非严格模式之间的区别主要是以下三点：
- 在严格模式中**禁止使用with语句**。
- 在严格模式中，**所有变量都要声明**。如果给一个未声明的变量、函数、**函数参数、catch从句参数**（这两个我需要实例验证一下）或者全局对象的属性赋值，将会抛出一个引用错误异常。
- 在严格膜使用，调用函数（不是方法）中的`this`值是undefined。（在非严格模式中，调用的函数中的this值总是全局对象）。可以利用这种特性来判断Javascript实现是否支持严格模式：
```
var hasStrictMode = (function() { "use strict";return this === undefined }())
```
