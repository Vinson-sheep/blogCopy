---
title: 讨论CSS伪元素的父元素
date: 2017-10-20 23:33:52
categories: "前端"
tags:
     - CSS
     - 原创
description: no
---

为什么要讨论css中伪元素的父元素呢？因为很多时候需要用到position属性，而position属性效果跟父元素直接挂钩。这篇文章就是讨论CSS中伪元素的父元素到底是谁？
<!--more-->

## 什么是伪元素？
参考[菜鸟教程](http://www.runoob.com/css/css-pseudo-elements.html)列出所有的伪元素
- :link
- :visited
- :active
- :focus
- :first-letter
- :first-line
- :first-child
- :before
- :after
- lang(language)

## 测试1

以`:first-letter`写一段html和css：
```
// html
<p id="test">假猪套天下第一</p>
// css
<style>
#test {
    font-size: 15px;  
}
#test:first-letter {
    font-size: 20px;
}
</style>
```
在浏览器中测试以上代码：

![测试结果](http://ohkgqh4gv.bkt.clouddn.com/1508514453%281%29.png)

很明显，`#test:first-letter`覆盖了`#test`的CSS样式。

所以`#test:first-letter`是`#test`的子元素。

神马？证明还不够充分？再来！

## 测试2
拿[菜鸟教程](http://www.runoob.com/try/try.php?filename=trycss_buttons_animate1)的一个例子：
```
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>菜鸟教程(runoob.com)</title>
<style>
.button {
  display: inline-block;
  border-radius: 4px;
  background-color: #f4511e;
  border: none;
  color: #FFFFFF;
  text-align: center;
  font-size: 28px;
  padding: 20px;
  width: 200px;
  transition: all 0.5s;
  cursor: pointer;
  margin: 5px;
}

.button span {
  cursor: pointer;
  display: inline-block;
  position: relative;
  transition: 0.5s;
}

.button span:after {
  content: '»';
  position: absolute;
  opacity: 0;
  top: 0;
  right: -20px;
  transition: 0.5s;
}

.button:hover span {
  padding-right: 25px;
}

.button:hover span:after {
  opacity: 1;
  right: 0;
}
</style>
</head>
<body>

<h2>按钮动画</h2>

<button class="button" style="vertical-align:middle"><span>Hover</span></button>

</body>
</html>
```
仔细观察
```
.button span:after {
    position: absolute;
}
```
和
```
.button span {
    position: relative;
}
```
就relative和absolute的前后关系，可以直接表明`span`是`span:after`的父元素。
