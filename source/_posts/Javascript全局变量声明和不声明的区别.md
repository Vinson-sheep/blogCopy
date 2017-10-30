---
title: Javascript全局变量声明和不声明的区别
date: 2017-09-30 15:41:12
categories: "前端"
tags:
     - javascript
description:
---

> 在非严格模式下，利用var声明全局变量，和不用var声明直接赋值，两者在普通的使用上几乎是一样的。唯一的区别是能够被delete。
<!--more-->

当声明一个Javascript全局变量时，实际上是定一个全局变量的属性。

当使用`var`声明一个变量时，创建的这个属性是不可配置的，也就是收这个变量**无法通过delete运算符删除**。

如果你没有使用严格模式并给一个未声明的变量赋值的话，Javascript会自动创建一个全局变量。以这种方式创建的变量是全局对象的正常的**可配值属性**，并可以删除它们：

下面分别通过不同的方式创建全局变量：
```
var truevar = 1;  // 声明一个不可删除的全局变量
fakevar = 2;  //创建全局对象的一个可删除属性
this.fakevar2 = 3;  // 同上
```
利用`delete`删除变量
```
delete truevar  // => false
delete fakevar  // => true
delete this.fakevar2  // => true
```
`true`: 变量被删除
`false`: 变量并没有被删除
