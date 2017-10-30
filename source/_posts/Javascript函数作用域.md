---
title: Javascript函数作用域
date: 2017-09-30 15:05:25
categories: "前端"
tags:
     - javascript
description:
---

> 在一些类似C语言的编程语言中，花括号内的每一段代码都具有各自的作用域，而且变量在声明它们的代码段之外是不可见的，我们称为**块级作用域**，而Javascript没有块级作用域的概念，取而代之的是函数作用域。——摘录自犀牛书
<!--more-->

Javascript的函数作用域是指函数内声明的所有变量在函数体内始终是可见的。有意思的是，这意味着变量在声明之前甚至已经可用。Javascript的这个特性被非正式地成为**声明提前**，即Javascript函数里生命的所有变量都被“提前”至函数体的顶部。

来看以下代码：
```
var scope = "global";
function f() {
    console.log(scope); // 输出"undefined"，而不是"global"
    var scope = "local";  
    console.log(scope); // 输出"local"
}
```
你可能会误以为函数中的第一行会输出"global"，因为代码还没执行到var语句声明局部变量的地方。其实不然，由于函数作用域的特性，局部变量在整个函数体始终是有定义的，也就是说，**在函数体内局部遮盖了同名全局变量**。尽管如此，只有在程序执行到var语句的时候，局部变量才真正赋值。因此，上述过程等价于： **将函数内的变量声明“提前”至函数体顶部，同时变量初始化留在原来的位置**：
```
function f() {
    var scope;
    console.log(scope);
    scope = "local";
    console.log(scope);
}
```

————以上摘录自《Javascript权威指南》

总结：为了避免**声明提前**而使访问值变为`undefined`，尽可能地在狭小的作用域中让变量声明和使用变量的代码尽可能靠近彼此。
