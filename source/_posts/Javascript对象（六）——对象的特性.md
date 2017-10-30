---
title: Javascript对象（六）——对象的特性
date: 2017-10-05 21:10:28
categories: "前端"
tags:
     - javascript
     - js对象
description:
---

> 对象的属性除了包含名字和值之外，属性还包含一些标识它们可写、可枚举和可配置的特性。在ECMAScript 3中无法设置这些特效。而ECMAScript 5中查询和设置这些属性特性的API。这些API对于库开发者来说非常重要。
<!--more-->

## 数据属性的4个特性
- 值(value)
- 可写性(writable)
- 可枚举性(enumerable)
- 可配置性(configurable)

## 存取器属性的4个特性
- 读取(get)
- 写入(set)
- 可枚举性
- 可配置性

## Object.getOwnPropertyDescriptor()
通过调用`Object.getOwnPropertyDescriptor()`可以获得某个对象特定属性的属性描述符：
```
// 返回 {value: 1,writable: true,enumerable: true,configurable: true}
Object.getOwnPropertyDescriptor({x:1}, "x");

// 查询上下文中定义的random对象的octet属性（这里没有random对象）
// 返回 { get: /*func*/, set:undefined, enumerable: true, configurable: true}
Object.getOwnPropertyDescriptor(random, "octet");

// 对于继承属性和不存在的属性，返回undefined
Object.getOwnPropertyDescriptor({}, "x");         // undefined,没有这个属性
Object.getOwnPropertyDescriptor({}, "toString");  // undefined,继承属性
```
从函数名字就可以看出，`Object.getOwnPropertyDescriptor()`只能得到自有属性的描述符。

## Object.defineProperty()
要想设置属性的特性，或者想让新建属性具有某种特效，则需要调用`Object.defineProperty()`，传入要修改的对象、要创建或修改的属性的名称以及属性描述符对象：
```
var o = {}; // 创建一个空对象
// 添加一个不可枚举的属性x，并赋值为1
Object.defineProperty(o, "x", { value: 1,
                                writable: true,
                                enumerable: false,
                                configurable: true});

// 属性是存在的，但不可枚举
o.x;            // => 1
Object.keys(o)  // => []

// 现在对属性x做修改，让它变为只读
Object.defineProperty(o, "x", {writable: false });

// 试图更改这个属性的值
o.x = 2;  // 操作失败但不报错，而在严格模式中抛出类型错误异常
o.x       // => 1

// 属性依然是可配置的，因此可以通过这种方式对它进行修改：
Object.defineProperty(o, "x", {value: 2});
o.x       // => 2

//现在将x从数据属性修改为存取器属性
Object.defineProperty(o, "x", { get: function() {return 0; }});
o.x       // => 0
```
传入`Object.defineProperty()`属性描述符对象不必包含所有4个特效。**对于新创建的属性来说，默认的特性值是false或undefined**。注意，这个方法要么修改已有属性要么新建自有属性，但不能修改继承属性。

## Object.defineProperties()
如果要同时修改或创建多个属性，则需要使用`Object.defineProperties()`。
```
var p = Object.defineProperties({},{
      x: {value: 1, writable: true, enumerable: true, configurable: true},
      y: {value: 1, writable: true, enumerable: true, configurable: true},
      r: {
          get: function() {return Math.sqrt(this.x*this.x + this.y*this.y) },
          enumerable: true,
          configurable: true
      }
});
```
这段代码从一个空对象开始，然后给它添加两个数据属性和一个只读存取器属性。最终`Object.defineProperties()`返回修改后的对象（和`Object.defineProperty`一样）。

## 配置规则
- 如果对象是不可扩展，则可以编辑已有的自有属性，但不能给它添加新属性。
- 如果属性是不可配置的，则不能修改它的可配置性和可枚举性。
- 如果存取器属性是不可配置的，则不能修改其getter和setter方法，也不能将它转换为数据属性。
- 如果数据属性是不可配置的，则不能将它转换为存取器属性。
- 如果数据属性是不可配置的，则不能将它的可写性从false修改为true，但可以从true修改为false。
- 如果数据属性是不可配置且不可泄的，则不能修改它的值。然而可配置但不可写属性的值是可以修改的（实际上是先将它标记为可写的，然后修改它的值，最后转换为不可写的）。
