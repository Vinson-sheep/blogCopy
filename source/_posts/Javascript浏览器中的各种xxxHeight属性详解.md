---
title: Javascript浏览器中的各种xxxHeight属性详解
date: 2017-10-12 23:48:16
categories: "前端"
tags:
     - javascript
     - js客户端对象
     - 原创
description:
---

> 曾经一度被浏览器中的各种高度弄得头晕眼花，今天特意查询了这方面的内容，终于搞懂了，决定写篇文章纪念一下scrollHeight、clientHeight、offsetHeigh、scrollTop、window.innerHeight、window.pageYOffset。
<!--more-->

*博主原创*

文章提要：

1. 滑动条的高度或宽度为17px
2. 这里讨论的xxxHeight返回的都是数值
3. 文章是以chrome测试作为结果，其他浏览器的说明是通过其他文章的描述总结得出。

## 通用属性
### 1. scrollHeight
scrollHeight表示的是滑动条内可滑动的内容。

如果内容没有超出元素高度，那么scrollHeight表示的是元素的height加上padding，不包括bording。

如果内容超出了元素高度但没有设置滑动条，那么scrollHeight表示的是元素height加上元素的上padding（scrollWidth为左padding），不包括下padding和bording。

如果内容超出了元素高度并且设置有滑动条，那么scrollHeight表示的是滑动条可滑动的高度，不包括滑动条自身的高度（17px）。

我们来测试一下：
```
<!DOCTYPE html>
<html>
<head>
    <title></title>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
    <style type="text/css">
        #test {
            width: 50px;
            border: 5px solid green;
            background-color: black;
            color: red;
            padding: 10px;
            overflow: scroll;
        }
    </style>
</head>
<body>

<div id="test">
    <span>clientHeight:可见区域的宽度,不包括boder的宽度,如果区域内带有滚动条,还应该减去横向滚动条不可用的高度,正常的是17px
    </span>
</div>

<script type="text/javascript">
    var test = document.getElementById("test");
    console.log("scroll=" + test.scrollHeight+ ";client=" + test.clientHeight + ";offset=" + test.offsetHeight)
</script>
</body>
</html>
```
下面是测试结果：

![chrome测试结果](http://ohkgqh4gv.bkt.clouddn.com/1507825158%281%29.png)
![console输出结果](http://ohkgqh4gv.bkt.clouddn.com/1507825190%281%29.png)

分析：

这里的例子是利用一些巧妙的方法，使保证内容全部显示的同时保持滑动条的存在。从图中我们可以看到，元素总导高度为551px，那么scrollHeight的数值到底是怎么算出来的呢？首先是上下border一共10px，再加上滑动条高度的17px一共27px，于是551-27=524。

最后引用其他博主的文字：
> scrollHeight:这个属性就比较麻烦了,因为它们在火狐跟IE下简直差太多了..
在火狐下还很好理解,它其实就是滚动条可滚动的部分还要加上boder的高度还要加上横向滚动条不可用的高度,与clientHeight比起来,多个border的高度跟横向滚动条不可用的高度.

>在IE中 scrollHeight确是指这个对象它所包含的对象的高度加上boder的高度和marging,如果它里面没有包含对象或者这个对象的高度值未设置,那么它的值将为15

### 2. clientHeight
这个属性等于元素内容高度height加上padding。

这个元素没什么好说的，各种浏览器下表现一样。

### 3. offsetHeight
这个属性表示元素内容高度height加上padding再加上border，但不包括margin。

### 4. scrollTop
这个属性表示视窗上面隐藏了部分的高度。

常用的语句是：`document.body.scrollTop`和`document.documentElement.scrollTop`

值得注意的一点是，chrome不承认`document.documentElement.scrollTop`，或者说，它永远返回数值`0`。

## 浏览器对象属性
### 1. window.innerHeight
返回浏览器窗口高度。

### 2. window.pageYOffset
数值和`document.body.scrollTop`一致，表示视窗上面隐藏了部分的高度。

参考文章：

[JS实现无限分页加载——原理图解](http://www.cnblogs.com/xing901022/p/5052780.html)

[height、clientHeight、scrollHeight、offsetHeight区别](http://www.cnblogs.com/yuteng/articles/1894578.html)

[Chrome不认documentElement.scrollTop](https://jingyan.baidu.com/article/a3f121e4f21433fc9052bb8f.html)
