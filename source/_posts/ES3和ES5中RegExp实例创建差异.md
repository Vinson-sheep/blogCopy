---
title: ES3和ES5中RegExp实例创建差异
date: 2017-10-13 21:56:51
categories: "前端"
tags:
     - javascript
     - RegExp
     - ES标准
description:
---

> 犀牛书中揭示了不同ES标准下RegExp实例创建的差异，虽然这种差异是很难被应用在实际开发中的。不过了解一下也无妨。
<!--more-->

```
// 正则表达式直接量
var pattern = /s$/
```

正则表达式直接量,ECMAScript 3规范规定，一个正则表达式直接量会在执行到它的时候转换为一个RegExp对象，同一段代码所表示正则表达式直接量的每次运算都返回同一个对象。ECMAScript 5规范则做了相反的规定，同一段代码所代表的正则表达式直接量的每次运算都返回新对象。IE一直都是按照ECMAScript 5规范实现的，多数最新版本的浏览器也开始遵循ECMAScript 5，尽管目前该标准并未全面广泛推行。

*要知道犀牛书已经很旧了，实际上主流的浏览器几乎都遵循ES 5，有的甚至全面实现ES 6。*

犀牛书的作者在这里揭示了一种非常容易忽略的情况，比如，这段代码在Firefox 3.6和Firefox 4+中运行结果不一致：
```
function getRE() {
    var re = /[a-z]/;
    re.foo = "bar";
    return re;
}
var reg = getRE(),
    re2 = getRE();

console.log(reg == re2);  // 在Firefox .6中返回true，在Firefox 4+中返回false
reg.foo = "bar";
console.log(re2.foo); // 在Firefox 3.6中返回"baz"，在Firefox 4+返回"bar"
```

原因可以在ECMAScript 5规范第24页和第247页找到，也就是说在ECMAScript 3规范中，用正则表达式创建的RegExp对象会共享同一个实例，而在ECMAScript 5中则是两个独立的实例。而最新的Firefox 4、Chrome和Safari 5都遵循ECMAScript 5标准，以至于IE6~IE8都没有很好地遵循ECMAScript 3标准，不过在这个问题上反而处理对了。很明显ECMAScript 5的规范更符合开发者的期望。
