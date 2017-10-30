---
title: Javascript对象（一）——基本术语
date: 2017-10-05 01:03:03
categories: "前端"
tags:
     - javascript
     - js对象
description:
---

> 对象基本知识，方便看文章时候的理解。
<!--more-->

我们可以把对象看成是从字符串到值的映射。这种基本数据结构还有很多种叫法，有些我们已然非常熟悉，比如**“散射（hash）”、“散列表（hashtable）”、“字典（dictionary）”、“关联数组（associative）”**。

然而对象不仅仅是字符串到值的映射，除了可以保持自有的属性，Javascript对象还可以从一个成为原型的对象继承属性。对象的方法通常是继承的属性。**这种“原型式继承（prototypal inheritance）”是Javascript的核心特征**。

## 属性特性
- **可写**（writable attribute），表明是否可以设置该属性的值。
- **可枚举**（enumerable attribute），表明是否可以通过`for/in`循环返回该属性。
- **可配置**（configurable attribute），表明是否可以删除或修改该属性。

在ECMAScript 5之前，通过代码给对象创建的所有属性都是可写的、可枚举的和可配置的。

## 对象特性
- **对象的原型**（prototype）指向另一个对象，本对象的属性继承自它的原型对象。
- **对象的类**（class）是一个标识对象类型的字符串。
- **对象的扩展标记**（extensible flag）指明（在ECMAScript 5中）是否可以向该对象添加新属性。

## 三类JS对象+两类属性
- **内置对象**（native object）是由ECMAScript规范定义的对象或类。例如，数组、函数、日期和正则表达式都是内置对象。
- **宿主对象**（host object）是由Javascript解析器所嵌入的宿主环境（比如Web浏览器）定义的。客户端Javascript中表示网页结构的HTMLElement对象均是宿主对象。既然宿主环境定义的方法可以当成普通的Javascript函数对象，那么宿主对象也可以当成内置对象。
- **自定义对象**（user-defined object）是由运行中的Javascript代码创建的对象。
- **自有属性**（own property）是直接在对象中定义的属性。
- **继承属性**（inherited property）是在对象的原型对象中定义的属性。
