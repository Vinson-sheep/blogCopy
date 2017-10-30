---
title: Javascript中for/in循环机理
date: 2017-10-03 21:12:36
categories: "前端"
tags:
     - javascript
description:
---

> for/in循环是非常有用的原生语句，了解for/in循环的作用机理，可以实现意想不到的效果。
<!--more-->

## 基本语法
`for/in`语句也使用了`for`关键字，但它是和常规的`for`循环完全不同的一类循环。`for/in`循环语句的语法如下：
```
for (variable in object)
    statement
```
`for/in`循环是用来方便地遍历对象的属性成员。下面是`for/in`的一个实例：
```
for(var p in o) {
    console.log(o[p]);
}
```
在执行`for/in`语句的过程中，Javascript解析器首先计算Object表达式。如果表达式为`null`或者`undefined`，Javascript解析器将会跳过循环并执行后续的代码。

## 作用机理
只要`for/in`循环中variable的值可以当作赋值表达式的左值，它可以是任意表达式。**每次循环都会计算这个表达式，也就是说每次循环它计算的值都有可能不同。例如，可以使用下面这段代码将所有对象属性复制至一个数组中：
```
var o = { x:1,y:2,z:3};
var a = [],i = 0;
for (a[i++] in o) /* empty */ ;
```
分析：上面的`for/in`循环中，每一次循环都会将i加一，最关键的是，循环体object中的属性值会赋值给variable，所以每一次循环就会将object对应的值复制到数组a中去。

## 循环遍历
`for/in`循环并不会遍历对象的所有属性，只有“可枚举（enumerable）”的属性才会被遍历到。

在ECMAScript 5中可以通过特殊的手段让可枚举属性变为不可枚举的。

如果`for/in`的循环体删除了还未枚举的属性，那么这个属性将不会被枚举到。

如果循环体定义了对象的新属性，这些属性通常也不会被枚举到（然而,Javascript的有些实现是枚举这些在循环体内增加的继承属性）。

关于属性枚举的顺序，我也不是特别了解。在这里就不深入讨论了。
