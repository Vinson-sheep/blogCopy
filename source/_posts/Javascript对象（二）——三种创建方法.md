---
title: Javascript对象（二）——三种创建方法
date: 2017-10-05 01:03:45
categories: "前端"
tags:
     - javascript
     - js对象
description:
---

> 对象直接量、new创建对象、还有Object.create()方法创建对象。
<!--more-->

## 对象直接量
创建对象最简单的方式就是Javascript代码中使用对象直接量。
```
var empty = {};
```

## 通过new创建对象
```
var o = new Object(); // 创建一个空对象，和{}一样
```

## Object.create()
这个方法恐怕在开发JS库的时候才会用上。

ECMAScript 5定义了一个名为Object.create()的方法，它创建一个新对象，其中第一个参数是这个对象的原型。Objcet.create()提供第二个可选参数，用以对对象的属性进行进一步描述。
```
var o1 = Object.create({x:1, y:2}); //o1继承了属性x和y
```

可以通过传入参数`null`来创建一个没有原型的新对象，但通过这种方式创建的对象**不会继承任何东西，甚至不包括基础方法，比如toString()，也就是说，它将不能和“+”运算符一起正常工作**：
```
var o2 = Object.create(null); // o2不继承任何属性和方法
```

如果想要创建一个普通的空对象（比如通过`{}`或`new Object()`创建的对象），需要传入`Object.prototype`：
```
var o3 = Object.create(Object.prototype); // o3和{}和new Object()一样
```
