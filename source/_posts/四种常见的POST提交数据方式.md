---
title: 四种常见的POST提交数据方式
date: 2017-10-26 19:13:59
categories: "前端"
tags:
     - html
     - javascript
     - 表单
description:
---

> 最近看了一篇文章，相当有启发性，它解决了我对http请求中数据传输格式的困惑。在未来的表单页面制作，通过设置表单enctype属性能够实现更多的功能。上面也提及到json的前端设置，我觉得很有必要做做记录。
<!--more-->

*title说有四种常见的POST提交数据方式，其实有五种，最后一种不常见而已*

这里说到的POST方式，都可以作为数据的描述，使用ajax提交给服务器。

## application/x-www-form-urlencoded
这应该是最常见的POST提交数据方式了。

浏览器的原生 form 表单，如果不设置 enctype 属性，那么最终就会以 application/x-www-form-urlencoded 方式提交数据。请求类似于下面这样（无关的请求头在本文中都省略掉了）：
```
POST http://www.example.com HTTP/1.1
Content-Type: application/x-www-form-urlencoded;charset=utf-8

title=test&sub%5B%5D=1&sub%5B%5D=2&sub%5B%5D=3
```



## multipart/form-data
这又是一个常见的 POST 数据提交的方式。我们使用表单上传文件时，必须让 form 的 enctyped 等于这个值。直接来看一个请求示例：
```
POST http://www.example.com HTTP/1.1
Content-Type:multipart/form-data; boundary=----WebKitFormBoundaryrGKCBY7qhFd3TrwA

------WebKitFormBoundaryrGKCBY7qhFd3TrwA
Content-Disposition: form-data; name="text"

title
------WebKitFormBoundaryrGKCBY7qhFd3TrwA
Content-Disposition: form-data; name="file"; filename="chrome.png"
Content-Type: image/png

PNG ... content of chrome.png ...
------WebKitFormBoundaryrGKCBY7qhFd3TrwA--
```
这个例子稍微复杂点。首先生成了一个 boundary 用于分割不同的字段，为了避免与正文内容重复，boundary 很长很复杂。然后 Content-Type 里指明了数据是以 mutipart/form-data 来编码，本次请求的 boundary 是什么内容。消息主体里按照字段个数又分为多个结构类似的部分，每部分都是以 --boundary 开始，紧接着内容描述信息，然后是回车，最后是字段具体内容（文本或二进制）。如果传输的是文件，还要包含文件名和文件类型信息。消息主体最后以 --boundary-- 标示结束。

上面提到的这两种 POST 数据的方式，都是浏览器原生支持的，而且现阶段原生 form 表单也只支持这两种方式。但是随着越来越多的 Web 站点，尤其是 WebApp，全部使用 Ajax 进行数据交互之后，我们完全可以定义新的数据提交方式，给开发带来更多便利。

## application/json
application/json 这个 Content-Type 作为响应头大家肯定不陌生。实际上，现在越来越多的人把它作为请求头，用来告诉服务端消息主体是序列化后的 JSON 字符串。由于 JSON 规范的流行，除了低版本 IE 之外的各大浏览器都原生支持 JSON.stringify，服务端语言也都有处理 JSON 的函数，使用 JSON 不会遇上什么麻烦。
```
POST http://www.example.com HTTP/1.1
Content-Type: application/json;charset=utf-8

{"title":"test","sub":[1,2,3]}
```

## text/xml
```
POST http://www.example.com HTTP/1.1
Content-Type: text/xml

<!--?xml version="1.0"?-->
<methodcall>
    <methodname>examples.getStateName</methodname>
    <params>
        <param>
            <value><i4>41</i4></value>

    </params>
</methodcall>
```
我个人觉得 XML 结构还是过于臃肿，一般场景用 JSON 会更灵活方便。

## text/plain
在[菜鸟教程](http://www.runoob.com/tags/att-form-enctype.html)的描述是：
> 将空格转换为 "+" 符号，但不编码特殊字符。

其实实际开发中用得非常少，而且资料也不多，在这里不介绍了。


传送门：

[application/json 四种常见的 POST 提交数据方式](http://blog.csdn.net/tycoon1988/article/details/40080691)
