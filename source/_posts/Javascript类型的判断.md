---
title: Javascript类型的判断
date: 2017-10-08 22:26:53
categories: "前端"
tags:
     - Javascript
     - js对象
     - 原创
description:
---

> js对象的类型和类的判断，会让你头晕眼花的，起码我是这样。这篇文章通过原生和非原生的函数，将各种数据的类型和类检测出来，其中涉及到“鸭式辩型”的概念。
<!--more-->

*博主原创*

## typeof()
我们首先来看一下实例：
```
typeof undefined      // => "undefined"
typeof true           // => "boolean"
typeof NaN            // => "number"
typeof "abc"          // => "string"
typeof(function(){})  // => "function"

typeof null           // => "object"
typeof {}             // => "object"
typeof []             // => "object"
typeof(new Date)      // => "object"
typeof(/./）          // => "object"
typeof window         // => "object"

// 自定义对象
function f(name) { this.name=name; }
var fo = new f("vinson");
typeof fo;            // => "object"
```
从上面实例可以看到，使用js原生的运算符`typeof`，能分辨大部分的基本数据类型，但不能分辨类，即class。对于涉及原型链上的类，它一律返回"object"。

更重要的是，面对大部分内置对象（除了function），它依然返回`object`。比如在JS中，Array类是继承于`Object`的，所以`Array`原型的原型链中最终指向于`Object`。显然，这与我们的预期不符。

*但是函数function却能返回，这不是很过分吗？*

基于上面的分析，我们编写了下一个更缜密的函数`classof()`，检查类属性。

*注意，类型type和类class是不同的概念。*

*资料参考《Javascript权威指南》p87~88*

## classof()
对象的类属性（class attribute）是一个字符串，用以表示对象的类型信息。ECMAScript 3和ECMAScript 5都未提供设置这个属性的方法，并且只有一种间接的方法可以查询它。默认的`toString()`方法（继承自Object.prototype）返回了如下这种格式的字符串：
```
[object class]
```
因此，要想获得对象的类，可以调用对象的`toString()`方法，然后提取已返回字符串的第8个到倒数第二个位置之间的字符。不过让人感到棘手的是，**很多对象继承的`toString()`方法重写了**，为了能调用正确的`toString()`版本，必须简介地调用`Function.call()`方法。下面是classof的实现：
```
// classof()函数
function classof(o) {
    if (o === null) return "Null";
    if (o === undefined) return "Undefined";
    return Object.prototype.toString.call(o).slice(8,-1);
}
```
下面是这个函数的实例：
```
classof(null)       // => "Null"
classof(1)          // => "Number"
classof("")         // => "String"
classof(false)      // => "Boolean"
classof({})         // => "Object"
classof([])         // => "Array"
classof(/./)        // => "Regexp"
classof(new Date()) // => "Date"
classof(window)     // => "Window"（这是客户端宿主对象）
function f() {};    // 定义一个自定义构造函数
classof(new f());   // => "Object"
```
通过classof()函数，我们能够分辨出除了继承对象之外的所有基本类型和内置对象。

对比typeof()函数可以发现，classof()返回的字符串都是以大写开头的。

*资料参考《Javascript权威指南》p139~140*

## type()
自定义的对象都不能通过上面的两个方法分辨出来，我们需要一种更精细的方法来检测对象的类。这里的类指的是构造函数的名称。

我们可以通过通过constructor属性获取函数对象，再将函数对象转换为字符串，从中获取构造函数的名称，即类名称。下面是完整的代码：
```
/**
 * 以字符串的形式返回o的类型
 * - 如果o是null，返回"null";如果o是NaN，返回"nan"
 * - 如果typeof所返回的值不是"object"，则返回这个值
 * - (注意，有一些Javascript的实现将正则表达式识别为函数)
 * - 如果o的类不是"Object"，则返回这个值
 * - 如果o包含构造函数并且这个构造函数具有名称，则返回这个名称
 * - 否则，一律返回"Object"
 **/
function type(o) {
    var t,c,n;  // type,class,name

    //处理null值的特殊情况
    if (o === null) return "null";

    // 另外一种特殊情况:NaN和它自身不相等
    if (o !== o) return "nan";

    //如果typeof的值不是"object"，则返回这个值
    if((t = typeof o) !== "Object") return c;

    //返回对象的类名，除非值为"Object"
    //这种方式可以识别出大多的内置对象
    if((c = classof(o)) !== "Object") return c;

    //如果对象构造函数的名字存在的话，则返回它
    if(o.constructor && typeof o.constructor === "function" &&
          (n = o.construcor.getName())) return n;

    //其他的类型都无法判别，一律返回"Object"
    return "Object";
}

//返回对象的类
function classof(o) {
    return Object.prototype.toString.call(o).slice(8,-1);
};

//返回函数的名字（可能是空字符串），不是函数的话就返回null
Function.prototype.getName = function () {
    if ("name" in this) return this.name;
    return this.name = this.toString().match(/function\s*([^(]*)\(/)[1];
};
```
这种使用构造函数来识别对象的类的做法和使用constructor属性一样有一个问题：**并不是所有的对象都具有constructor属性。此外，并不是所有的函数都有名字。如果使用不带名字的函数定义表达式定义一个构造函数，getName()方法则会返回空字符串：
```
//这个构造函数没有名字
var Complex = function(x,y) { this.r = x;this.i = y; }
//这个构造函数有名字
var Range = function Range(f,t) { this.from = f;this.to = t;}
```

*《Javascript权威指南》p213~214*

## 鸭式辩型
上文所描述的检测对象的类的各种技术多少都会有些问题，至少在客户端Javascript中是如此。解决办法就是规避这些问题：不要关注“对象的类是什么”，而是关注“对象能做什么”。这种思考问题的方式在Python和Ruby中非常普遍，成为“鸭式辩型”。
> 像鸭子一样走路、游泳并且嘎嘎叫的鸟就是鸭子。

*实例...略*

*《Javascript权威指南》p215~216*
