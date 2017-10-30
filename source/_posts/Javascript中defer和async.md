---
title: Javascript中defer和async
date: 2017-10-16 00:29:54
categories: "前端"
tags:
     - javascript
description:
---

> 说实话defer和async属性是很少时候会用上。这篇文章就是讲述它如何如何难被用上。
<!--more-->

## 知识点

**文档解析**在web中指的是html文档被下载后由浏览器引擎解析为DOM节点树的过程。

**阻塞**在web是指html文档解析受阻。当一个http请求被响应，首先下载html文件，再解析html文件。也就是说，html文件是肯定会被下载的，但是解析可能会受阻。

这里引用犀牛书的一段话：

> 当HTML解析器遇到`<script>`元素时，它默认必须先执行脚本，然后再恢复文档的解析和渲染。这对于内联脚本没什么问题（这里大概是指不需要下载直接执行），但如果脚本源代码是一个由src属性指定的外部文件，这意味着脚本后面的文档部分在下载和执行脚本之前，都不会出现在浏览器中。

作者在这里的表述很模糊，所谓“不会出现在浏览器中”，是指文档的文本内容已经载入，但是未被浏览器引擎解析为DOM树，而DOM树的生成是受Javascript代码执行的影响的，Javascript代码会“阻塞”页面UI的渲染。

脚本的执行只在默认情况下是同步和阻塞的。

## defer和async
```
<script defer src="deferred.js"></script>
<script async src="async.js"></script>
```
defer和async属性都像在告诉浏览器链接进来的脚本不会使用`document.write()`，也不会生成文档内容，因此浏览器可以在下载脚本时候继续解析和渲染文档。

defer属性使得浏览器延迟脚本的执行，直到文档的载入和解析完成，并可以操作。

async属性使得浏览器可以尽快地执行脚本，而不用在下载脚本时阻塞文档解析。

如果`<script>`标签同时有两个属性，同时支持两者的浏览器会遵从async属性并忽略defer属性。

## 分析
无论是defer和async属性，只有在脚本下载过程中可能阻塞文档解析的过程中才能够发挥作用，意味着`<script>`元素需要出现在文档一般元素之前（非html和body元素）。

在html和Javascript代码分离的哲学思想下，我们大多会把`<script>`元素放在文档底部，`html`和`body`元素之前。这时候defer和async属性就不能发挥作用了，因为js是同步解析的，当解析到`<script>`时，整个DOM树几乎已经解析完毕，并且渲染完成。

总的来讲，这两个元素用得不多，当`<script>`放在head时可能会用上。
