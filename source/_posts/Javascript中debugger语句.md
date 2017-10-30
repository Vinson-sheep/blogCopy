---
title: Javascript中debugger语句
date: 2017-10-04 23:49:12
categories: "前端"
tags:
     - javascript
description:
---

> debugger语句是实战中是为了方便调试用的，但是就我开发体验来说，使用debugger语句的可能性不大。
<!--more-->

`debugger`语句通常什么都不做。然而，当调试程序可用并运行的时候，Javascript解析器将会（非必须）以调试模式运行。

下面是使用的实例：
```
function f(o) {
    if (o === undefined) debugger;  // 这一行代码只是用于临时测试
    ...                             // 函数的其他部分
}
```
在chrome中测试以上代码：
```
f();    // 不输入参数值，触发debugger行为
```
这时候chrome会进入调试模式，并且指出调试语句。

> 在ECMAScript 5中,`debugger`语句正式加入到这门语言里。但在相当长的一段时间里，主流浏览器厂商已经将其实现了。注意，可用的调试器是远远不够的，`debugger`语句不会启动调试器。但如果调试器已经在运行中，这条语句才会真正产生一个断点。例如，如果使用Firefox的调试扩展插件Firebug，则并必须首先为待测试的网页启用Friebug，这样debugger语句才能正常工作。
