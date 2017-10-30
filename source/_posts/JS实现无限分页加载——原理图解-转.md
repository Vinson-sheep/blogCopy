---
title: JS实现无限分页加载——原理图解(转)
date: 2017-10-13 11:45:54
categories: "前端"
tags:
     - javascript
     - 前端组件开发
     - 转载
description:
---

> 由于网页的执行都是单线程的，在JS执行的过程中，页面会呈现阻塞状态。因此，如果JS处理的数据量过大，过程复杂，可能会造成页面的卡顿。传统的数据展现都以分页的形式，但是分页的效果并不好，需要用户手动点击下一页，才能看到更多的内容。有很多网站使用 无限分页 的模式，即网页视窗到达内容底部就自动加载下一部分的内容...
本篇就无限分页的实现模型，讲述其中奥妙。
<!--more-->

## 原理图

实现无限分页的过程大致如下：

1. 视窗滚动到底部

2. 触发加载，添加到现有内容的后面。

因此，可能会出现两种情况：

1. 当页面的内容很少，没有出现滚动条。

2. 当页面的内容很多，出现了滚动条。

针对这两种情况，需要理解几个概念：

scrollHeight即真实内容的高度；

clientHeight比较好理解，是视窗的高度，就是我们在浏览器中所能看到内容的高度；

scrollTop是视窗上面隐藏掉的部分

![](http://ohkgqh4gv.bkt.clouddn.com/12.png)

## 实现的思路
**1. 如果真实的内容比视窗高度小，则一直加载到超过视窗**
**2. 如果超过了视窗，则判断下面隐藏的部分的距离是否小于一定的值，如果是，则触发加载。（即滚动到了底部）**

## 代码样例
代码部分没有太多的内容，需要注意的是：
**1. 使用fixed定位加载框**
**2. 使用setTimeout定时触发判断方法，频率可以自定义**
**3. 通过 真实内容高度 - 视窗高度 - 上面隐藏的高度 < 20，作为加载的触发条件**

```
<!DOCTYPE html>
<html>
<head>
    <title>无限翻页测试</title>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
    <script src="http://apps.bdimg.com/libs/jquery/2.1.4/jquery.min.js"></script>
    <style type="text/css">
    #spinner{
        position: fixed;
        top: 20px;
        left: 40%;
        display: block;
        color: red;
        font-weight: 900;
        background-color: rgba(80, 80, 90, 0.22);
        padding-top: 20px;
        padding-bottom: 20px;
        padding-left: 100px;
        padding-right: 100px;
        border-radius: 15px;
    }
    </style>
</head>
<body>
    <div id="sample">
    </div>
    <div id="spinner">
        正在加载
    </div>
    <script type="text/javascript">
        var index = 0;
        function lowEnough(){
            var pageHeight = Math.max(document.body.scrollHeight,document.body.offsetHeight);
            var viewportHeight = window.innerHeight ||
                document.documentElement.clientHeight ||
                document.body.clientHeight || 0;
            var scrollHeight = window.pageYOffset ||
                document.documentElement.scrollTop ||
                document.body.scrollTop || 0;
            // console.log(pageHeight);
            // console.log(viewportHeight);
            // console.log(scrollHeight);
            return pageHeight - viewportHeight - scrollHeight < 20;
        }

        function doSomething(){
            var htmlStr = "";
            for(var i=0;i<10;i++){
                htmlStr += "这是第"+index+"次加载<br>";
            }
            $('#sample').append(htmlStr);
            index++;
            pollScroll();//继续循环
            $('#spinner').hide();
        }

        function checkScroll(){
            if(!lowEnough()) return pollScroll();

            $('#spinner').show();
            setTimeout(doSomething,900);

        }
        function pollScroll(){
            setTimeout(checkScroll,1000);
        }
        checkScroll();
    </script>
</body>
</html>
```

## 个人总结
1. 触发加载的条件始终是：真实内容高度 - 视窗高度 - 上面隐藏的高度 < 20，只要把握好scrollHeight、scrollTop等属性就可以手动从写代码。
2. index加载内容变化的关键，如果需要让服务器返回数据，诸如评论内容等，将index提交给服务器，作为一组数据的索引。如果所有内容加载完毕，则将index设置为特定值，这样使用js就能够不再触发加载。
3. 例子中使用了setTimeout,个人觉得使用setInterval会更好懂一些。但是它使用setTimeout也是很精妙，通过函数对这setTimeout互相调用，达到setInterval相同的效果。
4. 本文精华所在是pageHeight、viewportHeight、scrollHeight的定义，尽管我觉得它命名上很不符合语义，但是代码还是相当严密。
5. `document.documentElement.scrollTop`在chrome是永远返回`0`的。

传送门：
![JS实现无限分页加载——原理图解](http://www.cnblogs.com/xing901022/p/5052780.html)
