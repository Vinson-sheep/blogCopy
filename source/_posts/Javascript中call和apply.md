---
title: Javascript中call和apply
date: 2017-10-07 17:01:51
categories: "前端"
tags:
     - javascript
     - js函数
description:
---

> 我们可以将call()和apply()看作是某个对象的方法，通过调用方法的形式来间接调用函数。
<!--more-->

call()和apply()的第一个实参是要调用函数的母对象，它是调用上下文，在函数体内通过this来获得对它的引用。要想以对象o的方法来调用函数f()，可以这样使用call()和apply()。
```
f.call(o);
f.apply(o);
```
在ECMAScript 5 的严格模式中，call()和apply()的第一个实参都会变为this的值，哪怕传入的实参是原始值甚至是null或者undefined。在ECMAScript 3和非严格模式中，传入的null和undefined都会被全局对象代替，而其他原始值则会被相应的包装类型所代替。

## call()
对于call()来说，第一个调用上下文实参之后的所有实参就是传入待调用函数的值。
```
f.call(o,1,2);
```

## apply()
apply()方法和call()类似，但传入实参的形式和call()有所不同，它的实参都放入一个数组当中：
```
f.apply(o,[1,2]);
```
