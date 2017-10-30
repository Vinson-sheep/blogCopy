---
title: css更改表单控件光标颜色
date: 2017-10-22 00:35:50
categories: "前端"
tags:
     - CSS3
     - CSS
description: no
---

> 看到一个比较新颖的文章，记录一下。
<!--more-->

一般表单控件光标的颜色跟color属性是一致的。

如果想仅仅改变光标颜色，需要特殊的CSS设置。

一直以来要实现这样的效果都是依靠模拟来实现。主要借助于CSS的``-webkit-text-fill-color`让文本变成镂空的，即把其设置为`transparent`，记住了，不是直接将color的值设置为`transparent`。除此之外，还需要借助`text-shadow`的威力。直接上代码吧：
```
.form-control {
    color: red !important;
    text-shadow: 0px 0px 0px #495057;
    -webkit-text-fill-color: transparent;
}
```
到今天为止，我们不需要这么蛋疼了。CSS提供了一个属性`caret-color`，可以直接让我们控制input和textarea控件的光标颜色，甚至是可编辑的HTML元素，像这样的`<div contenteditable>`。如此一来，只需要在样式中添加：
```
input,
textarea,
[contenteditable] {
    color: #495057; /* 文本颜色 */
    caret-color: red; /* 光标颜色 */
}
```
`caret-color`较三行代码兼容性差些。


传送门：
[如何改变表单控件光标颜色](http://www.w3cplus.com/css/caret-color.html)
