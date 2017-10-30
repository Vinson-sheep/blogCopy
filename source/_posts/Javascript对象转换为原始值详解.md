---
title: Javascript对象转换为原始值详解
date: 2017-09-30 13:30:52
categories: "前端"
tags:
     - javascript
description:
---

> 对象到布尔值的转换非常简单，所有的对象（包括包装对象）都会转换为true。而对象到数字、对象到字符串，则涉及到两个方法：toString和valueOf，情况相当复杂。就此做知识归纳。
<!--more-->

所有的对象继承了两个转换方法。第一个是`toString()`,它的作用是返回一个反映这个对象的字符串。

另一个转换对象的函数是`valueOf()`。默认的`valueOf()`方法简单地返回对象本身。

下面对这两个函数进行详细分析：

## toString()
### 实例
不同的对象对`toString()`的实现不一样：
```
({x:1, y:2}).toString()   // => "[object, Object]"
[1,2,3].toString()    // => "1,2,3"
(function(x) { f(x); }).toString()    // => "function(x) {\n f(x);\n}"
/\d+/g.toString()   // => "/\\d+/g"
new Date(2010,0,1).toString()   // => "Fri Jan 01 2010 00:00:00 GMT-0800 (PST)"
```
从上面的实例可以发现，对于一般对象{}，函数返回的字符串确实没有太大价值意义。而function和RegExp直接返回的是实现定义和直接量字符串，Date对象则通过一定的规则转换后得到近似于直接量的字符串。数字[]则是使用了join(",")方法，将各个子值拼在一起。


## valueOf()
### 实例
```
({x:1, y:2}).valueOf()   // => Object {x: 1, y: 2} 对象
[1,2,3].valueOf()   // => [1, 2, 3]
(function f(x) { f(x); }).valueOf()    // => function f(x) { f(x); } 对象
/\d+/g.valueOf()   // => /\d+/g
new Date(2010,0,1).valueOf()   // => 1262275200000
```
对比`toString()`可以看到，`valueOf()`对数组、正则、函数、普通对象都只会返回他们自己本身。Date对象返回的是从1970年1月1日开始计算的毫秒数，属于数值类型。

## 对象与运算符
### 原则
和“==”一样， “<”运算符以及其他关系运算符也会做对象到原始值的转换，但除去日期对象的特殊情况。

任何对象都会首先尝试调用valueOf()，然后调用toString()。不管得到的原始值是否直接使用，它都不会进一步被转换为数字或字符串。

看下面例子：
```
(function f(){return}) > 1    // => false
(function f(){return}) < 1    // => false
(function f(){return}) = 1    // => false
```
函数对象先是经过`valueOf()`转换得到自身，再通过`toString()`获得`"function(x) {\n f(x);\n}"`的定义表达式，本质是一个字符串。字符串和一个数字比较都会获得`false`布尔值，由此解释上面的结果。

### 日期对象
在运算符前，日期对象类型的转换稍微不一样，可以观察下面例子：
```
var now = new Date();   // 创建一个日期对象
typeof (now + 1)    // => "string"
typeof (now - 1)    // => "number"
now == now.toString()   // => true
now > (now - 1)    // => true
```
在`+`号运算加合数字的时候，日期对象使用`toString()`会变换为字符串，再将`1`变成`"1"`字符串，通过`+`拼合，得到的结果为`"Sat Sep 30 2017 14:11:17 GMT+0800 (中国标准时间)1"`。而非使用`valueOf()`变成数值，在此基础上加一。在使用日期对象进行运算的时候，应该显式转换为数值，再进行运算。
