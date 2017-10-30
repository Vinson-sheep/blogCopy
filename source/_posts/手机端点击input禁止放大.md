---
title: 手机端点击input禁止放大
date: 2017-09-22 22:28:41
categories: "前端"
tags:
     - CSS
description:
---

> 当点击手机表单，手机会自动放大，将窗口锁定到表单组件。为了让自己的网页看起来更像一个原生的app，我决定把手机发大这一默认行为禁掉。

如果不作特殊设置，在手机端的表单输入文本框会在被点击后放大，如果想取消这一行为，可以在头部加上：
```
<meta name="viewport" content="width=720,inital-scale=1.0,user-scalable=no;">
```
再加上css样式：
```
input,input:focus,input:active{user-select: text;}
```
