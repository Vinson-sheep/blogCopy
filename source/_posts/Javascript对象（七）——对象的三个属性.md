---
title: Javascript对象（七）——对象的三个属性
date: 2017-10-05 23:45:21
categories: "前端"
tags:
     - javascript
     - js对象
description:
---

> 对象的三个属性：原型属性、类属性、可扩展性。
<!--more-->

## 原型属性
获取原型对象：
```
Object.prototype
```
查询原型：
```
Object.getPrototypeOf()
```
查询构造函数：
```
o.constructor
```
检测是否是某对象原型：
```
var p = {x:1};
var o = Object.create(p);
p.isPrototypeOf(o);   => true
Object.prototype.isPrototypeOf(o);  => true
```

## 类属性
对象的类属性（class attribute）是一个字符串，用以表示对象的类型信息。**ECMAScript 3和ECMAScript 5都未提供设置这个属性的方法，并和自由一种间接的方法可以查询它**。默认的`toString()`方法返回了如下这种格式的字符串：
```
[object class]
```
因此可以编写`classOf`函数：
```
function classof(o) {
    if (o===null) return "Null";
    if (o===undefined) return "Undefined";
    return Object.prototype.toString.call(o).slice(8,-1);
}
```
由于很多对象的`toString()`方法重写了，所以利用`call()`调用最原始的`toString()`函数。

下面是这个函数执行的例子：
```
classof(null)       // => "Null"
classof(1)          // => "Number"
classof("")         // => "String"
classof(false)      // => "Boolean"
classof({})         // => "Object"
classof([])         // => "Array"
classof(/./)        // => "RegExp"
classof(new Date()) // => "Date"
classof(window)     // => "Window"(这是客户端宿主对象)
function f() {};    // 定义一个自定义构造函数
classof(new f())    // => "Object"
```

## 可扩展性
对象的扩展性用以表示是否可以给对象添加新属性。**所有内置对象和自定义对象都是显式可扩展的，宿主对象的可扩展性是由Javascript引擎定义的**。

### Object.preventExtensions()
通过将对象传入`Object.preventExtensions()`，将对象转换为不可扩展的。

注意，一旦将对象转换为不可扩展的，就无法将其转换回可扩展的了。

同样需要注意的是，`preventExtensions()`只影响到对象本身的可扩展性。如果给一个不可扩展的对象的原型添加属性，这个不可扩展的对象同样会继承这些新属性。

判断函数`Object.isExtensions()`

### Object.seal()
`Object.seal()`和Object.preventExtensions()类似，除了能够将对象设置为不可扩展的，还可以将对象的所有自有属性都设置为不可配置的。

判断函数`Object.isSealed()`

### Object.freeze()
`Object.freeze()`将更严格地锁定对象——“冻结”（frozen）。除了对象设置为不可扩展的和将其属性设置为不可配置之外，还可以将它自由的所有数据属性设置为只读。

判断函数`Object.isFrozen()`
