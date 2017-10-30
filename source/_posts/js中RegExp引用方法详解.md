---
title: js中RegExp引用方法详解
date: 2017-10-14 18:43:13
categories: "前端"
tags:
     - javascript
     - RegExp
description:
---

> 归纳总结一些能够引用RegExp的方法，包括正则表达式对象的属性。
<!--more-->

## String方法
1. search()
2. replace()
3. match()
4. split()

## RegExp对象属性
1. source
2. global
3. ingoreCase
4. multiline
5. lastIndex

## RegExp对象方法
1. exec()
2. test()

***

## 详解
### lastIndex
lastIndex是一个可读/可写的整数。在全局模式下使用exec()或者test()，会调用lastIndex属性，如果它找到一个匹配结果，那么它就立即设置lastIndex为当前匹配字串的结束位置。

### exec()和test()
其实这两个函数行为是一致的，在全局模式g下能够引用RegExp对象的lastIndex属性。我们可以看下面的例子：
```
// 定一个字符串
var s = "123";
// 声明一个正则表达式
var pattern = /\d/g;
// 匹配的是1，返回true
pattern.test(s);
// 匹配的是2，返回"2"
pattern.exec(s)
// lastIndex经过两次递增后为2
pattern.lastIndex;  // => 2
```
值得注意的是，全局模式下使用test()或者exec()时，如果没有匹配到任何内容，则返回`null`，同时lastIndex会自动刷新为0。当然lastIndex是可以显示更改的。

### exec()和match()
这两个函数在没有匹配项的时候会返回`null`，否则一律返回数组，即使只有一个匹配项。

exec()不能够一次得到所有匹配项。如果需要获取字符串所有的匹配项，需要在全局模式g下使用循环，这时候函数会自动调用lastIndex属性。当函数返回为`null`，证明已经遍历了整个字符串。

match()能够一次得到一个由所有匹配项得到的数组。分组()只要不影响正则表达式的逻辑，不会对输出结果个数造成影响。
```
// 无分组
"abcabc".match(/abc/g);   // => ["abc", "abc"]
// 分组
"abcabc".match(/(abc)/g); // => ["abc", "abc"]
```
综合地说，exec()适合获取分组，match()适合一次获取所有的匹配项。
