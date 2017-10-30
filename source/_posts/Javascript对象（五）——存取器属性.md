---
title: Javascript对象（五）——存取器属性
date: 2017-10-05 19:34:06
categories: "前端"
tags:
     - javascript
     - js对象
description:
---

> 由getter和setter定义的属性称作“存取器属性”（accessor property），它不用于“数据属性”（data property），数据属性只有一个简单的值。
<!--more-->

在ECMAScript 5（包括除了IE之外的最新主流浏览器的ECMAScript 3的实现）中,属性值可以用一个或两个方法替代，这两个方法就是`getter`和`setter`。

和数据属性不同，存取器属性不具有可写性。如果属性同时具有getter和setter方法，那么它是一个读/写属性。如果它只有getter方法，那么它是一个只读属性。如果它只有setter方法，那么它是一个只写属性（数据属性中有一些例外），读取只写属性总是返回`undefined`。

定义存取器属性最简单的方法是使用对象直接量语法的一种扩展写法：
```
var o = {
    // 普通的数据属性
    data_prop: value,

    // 存取器属性都是成对定义的函数
  get accessor_prop() { /*这里是函数体 */},
set accessor_prop(value) { /*这里是函数体*/}
}
```

**注意：**
存取器属性定义为一个或两个和属性同名的函数，这个函数定义没有使用function关键字，而是使用get和（或）set。注意，这里没有使用冒号将属性名和函数体分隔开，但在函数提的结束和下一个方法或数据属性之间有逗号分隔。

在ECMAScript 5中，可以通过`Object.getOwnPropertyDescriptor()`和`Object.defineProperty()`来修改getter和setter方法。
