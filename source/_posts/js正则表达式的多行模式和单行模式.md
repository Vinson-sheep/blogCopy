---
title: js正则表达式的多行模式和单行模式
date: 2017-10-14 15:05:42
categories: "前端"
tags:
     - javascript
     - RegExp
     - 原创
description:
---

> 参考了一些文章，对js正则表达式的多行模式和单行模式有了更深的了解。
<!--more-->

## 引言
其实底部的文章已经把多行模式和单行模式的关系讲述得很透彻了，但是它是针对php和Expresso，在js环境下的正则表现会有差异。多行模式在犀牛书的描述其实也是相当简洁明了的：
> 修饰符“m”用以在多行模式中执行匹配，在这种模式下，如果检索的字符串包含多行，那么^和$锚字符除了匹配整个字符串的开始和结尾之外，还能匹配每行的开始和结尾。

书上这么说，但到底是怎么一种情况呢？

## 文本保存的方式
首先我们来思考一个问题，当我们在win上的txt文本上敲一个回车然后保存，那文件对回车的保存是如何实现的？

![比如我在这输入点东西](http://ohkgqh4gv.bkt.clouddn.com/1507965279%281%29.png)

知识点：`\r`为回车符，`\n`为换行符。

在windows中，我们平常说的换行，实质上是先回车，后换行。

所以上图的文本等价于`1abcde\r\n2abc\r\n3eeeee\r\n`。


我们可以基于上面的讨论，在js中模拟多行文本。

## 测试
真实的测试是需要调用本地或者网络文件，读取里面的内容再进行多行匹配。

为了便于测试，我们使用`1abcde\r\n2abc\r\n3eeeee\r\n`进行测试。

下面的测试代码：
```
<script type="text/javascript">
    var pattern = /^(\d\w+)$/mg;

    var item = "1abcde\r\n2abc\r\n3eeeeee";
    var item1 = "1abcde\n2abc\n3eeeeee";
    var item2 = "1abcde\r2abc\r3eeeeee";

    console.log(item.match(pattern));
    console.log(item1.match(pattern));
    console.log(item2.match(pattern));
</script>
```
输出结果：`["1abcde", "2abc", "3eeeeee"]`

分析： 如果你阅读了尾部的文章，你会发现输出结果差异非常大，后面会讨论这个问题。在这个例子中，我们分别测试了混合使用`\r\n`与单独使用`\r`和`\n`的情况，结果输出均为`["1abcde", "2abc", "3eeeeee"]`。这表明，js多行模式下，`\n`和`\r`表现是相同的，`^`和`$`这两个锚元素都可以定位`\n`和`\r`前后。

## 对 . 符号的影响
我们将上面的代码修改一下：
```
<script type="text/javascript">
    var pattern = /^.$/gm;
    var item = "a";
    var item1 = "\n";
    var item2 = "\r";
    console.log(item.match(pattern));
    console.log(item1.match(pattern));
    console.log(item2.match(pattern));
</script>
```
输出结果：`["a"]`、`null`、`null`。

那是不是表明多行模式下`.`不能匹配`\n\r`呢？别急，我们将代码再改改：
```
    var pattern = /^.$/g;
```
输出结果：`["a"]`、`null`、`null`。

结果令人有点惊讶，单双行模式下`.`的表现是一致的。如果查看尾部文章，可以发现测试结果与尾部文章的差异甚大。

*为什么要做这个测试？因为参考文章提及到这个问题*

## 结论
1. 多行模式会影响`^`和`$`的匹配，而且对`\n`和`\r`的表现是一样的。
2. 正则表达式中的`.`符号是不能够匹配`\n`和`\r`，无论是单行还是多行模式下。
3. php和Expresso对正则的实现与js的差异非常大，要理解语言的特殊性。







传送门：

[正则表达式的多行模式与单行模式](http://blog.csdn.net/zm2714/article/details/7925264)
