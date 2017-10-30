---
title: Javascript中eval()函数详解
date: 2017-10-03 14:33:34
categories: "前端"
tags:
     - javascript
description:
---

> eval()是一个函数，但它已经被当成是运算符来对待了。如果一个函数调用了eval()，那么解析器将无法对这个函数进行优化。eval()函数可以用来使用制作在线的Javascript解析器，或者是作手动的函数优化。
<!--more-->

## eval()
`eval()`只有一个参数。如果传入的参数不是字符串，它直接返回这个参数。如果参数是字符串，它会把字符串当成Javascipt代码进行编译。

关于eval()最重要的是，它使用了调用它的变量作用域环境。也就是说，它查找变量的值和定义新变量和函数的操作和局部作用域中的代码完全一样。

如果在最顶层代码中调用`eval()`，当然，它会作用于全局变量和全局函数。

## 全局eval()
ECMAScript 3标准规定了任何解析器都不允许对`eval()`赋予别名。如果eval()函数通过别名调用的话，则会抛出一个EvalError异常。

事实上，大多数的实现并不是这么做的。

**当通过别名调用的时候，`eval()`会将其字符串当成顶层的全局代码来执行**。执行的代码可能会定义新的全局变量和全局函数。

> ECMAScript 5是反对使用EvalError的，并且规范了`eval()`的行为。“直接的eval”，当直接使用非限定的“eval”名称（eval看起来像是一个保留字）来调用eval()函数时，通常成为“直接eval”。直接调用`eval()`时，它总是在调用它的上下文作用域内执行。其他的间接调用则会使用全局对象作为其上下文的作用域，并且无法读、写、定义局部变量和函数。 ——摘录自《Javascript权威指南》

上面这段话很长，但是我们可以用简洁的语言归纳：ES 5在打ES 3的脸，浏览器对ES 3的抗议获得大成功，ES 5将大部分浏览器对eval()的实现纳入了标准。

下面有一段示例代码：
```
var geval = eval;               // 使用别名调用eval将会是全局eval
var x = "global",y = "global";  // 两个全局变量
function f() {                  // 函数内执行的是局部eval
    var x = "local";            // 定义局部变量
    eval("x += 'changed';");    // 直接eval更改了局部变量和值
    return x;                   // 返回更改后的局部变量
}               
function g() {                  // 这个函数内执行了全局eval
    var y = "local";            // 定义局部变量
    geval("y += 'changed';");   // 间接调用改变了全局变量的值
    return y;                   // 返回未更改的局部变量
}
console.log(f(), x);            // "localchanged global"
console.log(g(), y);            // "local globalchanged"
```

## 严格eval()
ECMAScript 5严格模式对`eval()`施加更多的限制。

严格模式下，eval执行的代码段可以查询或更改局部变量，但不能在局部作用域中定义新的变量或函数。

此外，严格模式将"eval"列为保留字，这让`eval()`更像一个运算符。不能用一个别名覆盖eval()函数。并且变量名、函数名、函数参数或者异常捕获的参数都不能取名为"eval"。
