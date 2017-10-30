---
title: Javascript对象（四）——检测属性
date: 2017-10-05 18:22:26
categories: "前端"
tags:
     - javascript
     - js对象
description:
---

> in运算符、hasOwnProperty()方法和propertyIsEnumerable()方法。顺便介绍另外两个偏门的枚举属性的方法：Object.keys()和Object.getOwnPropertyNames()。
<!--more-->

## in运算符
in运算符的左侧是属性名（字符串），右侧是对象。如果对象的自由属性或继承属性中包含这个属性则返回`true`。
```
var o = { x:1 };
"x" in o;     // true: "x"是o的属性
"y" in o;     // false: "y"不是o的属性
"toString" in o;  // true: o继承toString属性
```

出来使用in运算符之外，另一种更简便的方法是使用`“!==”`判断一个属性是否是`undefined`：
```
var o = { x: 1 };         
o.x !== undefined;          // true
o.y !== undefined;          // false
o.toString !== undefined;   // true
```

然而有一种场景只能使用in运算符而不能使用上述属性访问的方式。in可以区分不存在的属性和存在但值为`undefined`的属性。例如下面的代码：
```
var o = { x: undefined }; //属性被显式赋值为undefined
o.x !== undefined;        // false
o.y !== undefined;        // false
"x" in o;                 // true
"y" in o;                 // false
delete o.x;               // 删除了属性x
"x" in o;                 // false
```

## hasOwnProperty()方法
对象的`hasOwnProperty()`方法是用来检测给定的名字是否是对象的自有属性。对于继承属性它将返回`false`:
```
var o = { x: 1 };
o.hasOwnProperty("x");  // true: o有一个自有属性x
o.hasOwnProperty("y");  // false: o中不存在属性y
o.hasOwnProperty("toString"); // false: toString是继承属性
```

## propertyIsEnumerable()方法
`propertyIsEnumerable()`是`hasOwnProperty()`的增强版，只有检测到是自有属性且这个属性的可枚举性为`true`时它才返回`true`。
```
var o = inherit({ y:2 });
o.x = 1;
o.propertyIsEnumerable("x");  // true: o有一个可枚举的自有属性x
o.propertyIsEnumerable("y");  // false: y是继承过来的
Object.prototype.propertyIsEnumerable("toString");  // false: 不可枚举
```

## 开个玩笑
看下面代码：
```
Object.prototype.hasOwnProperty("has.OwnProperty");  // => true
Object.prototype.hasOwnProperty("propertyIsEnumerable");  // => true
```

## Object.keys()
ECMAScript 5定义了两个用以枚举属性名称的函数。

第一个是`Object.keys()`,这个函数返回一个数组，这个数组由对象中可枚举的自由属性的名称组成。

## Object.getOwnPropertyNames()
这个函数返回对象的所有自有属性的名称，而不仅仅是可枚举的属性。
