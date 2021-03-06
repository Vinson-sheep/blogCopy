---
title: Javascript逻辑运算符——原理详解
date: 2017-10-01 00:38:48
categories: "前端"
tags:
     - javascript
description:
---

> 最开始我看廖学锋的javascript教程，以为&&是直接返回一个布尔值ture或者false，直到我膝盖中了一剪，遇到犀牛书，突然恍然大悟。
<!--more-->

## 逻辑与（&&）
犀牛书中描述了`&&`的第三层理解：

> 运算符首先计算左操作数的值，即首先计算“&&”左侧的表达式。如果计算结果是加值，那么整个表达式的结果一定是假值，因此“&&”这时简单地返回左操作数，并不会对右操作数进行计算。
>
>反过来讲，如果左操作数是真值，那么整个表达式的结果则依赖于右操作数的值。

*假值是`false`、`null`、`undefined`、`0`、`-0`、`NaN`和`""`*

```
var o = { x:1 };
var p = null;
o && o.x  // =>1:0 是真值，因此返回值为o.x
p && p.x  // =>null: p是假值，因此将其返回，并不去计算p.x
```

## 逻辑或（||）
尽管“||”运算大多情况下只是做简单布尔或（OR）运算，和“&&”一样，它也具有一些更复杂的行为。

它会首先计算第一个操作数的值，也就是说会首先计算左侧的表达式。如果计算结果为真值，那么返回这个真值。否则，再计算第二个操作数的值，即计算右侧的表达式，并返回这个表达式的计算结果。

```
// 如果max_width已经定义了，直接使用它
// 否则在preferences对象中查找max_width
// 如果没有定义它，则使用一个写死的常量
var max = max_width || preferences.max_width || 500;
```

## 逻辑非（!）
“!”运算符首先将其操作数转换为布尔值，然后再对布尔值求反。

也就是说“!”总是返回`true`或者`false`。
