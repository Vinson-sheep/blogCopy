---
title: Javascript闭包
date: 2017-10-07 13:32:02
categories: "前端"
tags:
     - javascript
     - js闭包
description:
---

> 函数对象可以通过作用域链互相关联起来，函数体内部的变量都可以保存在函数作用域呢，这种特性在计算机科学文献中称为“闭包”。
<!--more-->

“闭包”，这个术语非常古来，是指函数变量可以被隐藏于作用域链之内，因此看起来是函数将变量“包裹”了起来。

*犀牛书p182~188*

## 作用域链规则
来看下这段代码：
```
var scope = "global"; // 全局变量
function checkscope() {
    var scope = "local scope";  // 局部变量
    function f() { return scope; }  //在作用域中返回这个值
    return f();
}
checkscope();       // => "local scope"
```
上面得出`local scope`应该毫无悬念。

现在我们对这段代码做小改动。
```
var scope = "global scope"; // 全局变量
function checkscope() {
    var scope = "local scope";  // 局部变量
    function f() { return scope; }
    return f;
}
checkscope()()  // 返回值是什么？
```
`checkscope`函数会返回一个内嵌函数，而执行这个引用了局部变量的内嵌函数，返回的是什么呢？不管在何时何地执行函数f()，f()和checkscope()函数的绑定依然有效。因此最后一行代码会返回`local scope`，而不是`global scope`。简而言之，闭包的这个特效强大得让人大吃一惊：它们可以捕捉到局部变量（和参数），并一直保存下来，看来像这里变量绑定到了在其中定义它们的外部函数。

## 私有变量
像counter一样的私有变量不是只能用在一个单独的闭包内，在同一个内部函数内定义的多个嵌套函数也可以访问它，这多个嵌套函数都共享一个作用域链，看一下这段代码：
```
function counter() {
    var n = 0;
    return {
        count: function() {return n++;},
        reset: function() {n=0;}
    };
}
var c = counter(), d = counter(); // 创建两个计数器
c.count()   // => 0
d.count()   // => 0 : 它们互不干扰
c.reset()   // reset()和count()方法共享状态
c.count()   // => 0
d.count()   // => 1: 而没有重置d
```

## 循环陷阱
先看下面代码：
```
// 这个函数返回一个总是返回v的函数
function constfunc(v) {return function() {return v;};}

// 创建一个数组用来储存常数函数
var funcs = [];
for (var i=0; i<10; i++) funcs[i] = constfunc(i);

// 在第5个位置的元素所表示的函数返回值为5
funcs[5]()  // => 5
```
这段代码利用循环创建了很多个闭包，当写类似这种代码的时候往往会犯一个错误：啊就是试图将循环代码移入定义这个闭包的函数之内，看一下这段代码：
```
// 返回一个函数组成的数组，它们的返回值是0~9
function constfuncs() {
    var funcs = [];
    for (var i = 0; i<10; i++)
        funcs[i] = function() { return i; };
    return funcs;
}

var funcs = constfuncs();
func[5]() // 返回值是什么？
```
上面这段代码创建了10个闭包，并将它们存储到一个数组中。这些闭包都是在同一个函数调用中定义的，因此它们可以共享变量i。当`constfuncs()`返回时，变量i的值是10，所有的闭包都共享这一个值，因此，数组中的函数的返回值都是同一个值，这不是我们想要的结果。**关联到闭包的作用域链都是“活动的”。**

## 注意
### this是Javascript的关键字，不是变量
每个函数调用都包含一个this值，如果闭包在外部函数里是无法访问this的，除非外部函数将this转存为一个变量：
```
var self = this;  // 将this保存至一个变量中，以便嵌套的函数能够访问它
```
### arguments并不是关键字
`arguments`并不是一个关键字，但在调用每个函数时都会自动声明它，由于闭包具有自己所绑定的`arguments`，因此闭包无法直接访问外部函数的参数数组，除非外部函数将参数数组保存到另一个变量中：
```
var outerArguments = argumens;  // 保存起来以便嵌套的函数能够使用它
```
