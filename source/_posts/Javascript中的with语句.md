---
title: Javascript中的with语句
date: 2017-10-04 23:20:52
categories: "前端"
tags:
     - javascript
description:
---

> 在实战中使用with语句，要注意几点。
<!--more-->

## with语句
`with`语句用于临时扩展作用域链，它具有以下的语法：
```
with (object)
statement
```
这条语句将object添加到作用域链的头部，然后执行statement，最后把作用域链恢复到原始状态。

## with不效率
在严格模式中是严格使用`with`语句的，并且在非严格模式里也是不推荐使用with语句的，尽可能避免使用`with`语句。

那些使用`with`语句的Javascript代码非常难于优化，并且同没有使用`with`语句的代码相比，它运行更慢。

对于对象嵌套层次很深的情况，使用`with`语句是可以简化代码编写，比如我们要访问HTML表单元素，我们可以这么做：
```
with(document.forms[0]) {
    // 直接访问表单元素，例如：
    name.value = "";
    address.value = "";
    email.value = "";
}
```
`with`小括号后面的对象会临时挂载在作用域链上，这样减少了大量的输入。

有时候为了便于优化代码或者提高性能，我们会使用替代的方法：
```
var f = document.forms[0];
f.name.value = "";
f.address.value = "";
f.email.value = "";
```

## with不能创建新属性
犀牛书上有一个例子：
```
with(0) x = 1;
```
书上的分析是这样的：
> 如果对象o有一个属性x，那么这行代码给这个属性赋值为1。但如果o中没有定义属性x，这段代码和不使用with语句的代码`x=1`是一模一样的。它给一个局部变量或者全局变量赋值，或者创建全局对象的一个新属性。with语句提供了一种读取o的属性的快捷方式，但它并不能创建o的属性。

为了便于理解，我在chrome浏览器的console中测试了以下例子：
```
var o = {};         // 定义一个新的空对象
with(o) x = 1;      // => 1:赋值成功
console.log(o.x);   // => undefined：未定义
console.log(x);     // => 1：数据绑定在全局对象中
```
根据这个例子再细读一次犀牛书的原话，应该有所收获。
