---
title: JQuery增删cookie
date: 2017-09-22 23:03:07
categories: "前端"
tags:
     - JQuery
     - cookie
     - javascript
description:
---
> 有一些项目需要大量部署cookie增删的代码，比如登录系统。通过使用jquery.cookie.js插件，实现JQuery对cookie的控制。
<!--more-->

## 引入jquery.cookie.js库文件
1. 下载jquery.cookie.js
[CSDN下载地址](http://download.csdn.net/download/mattwayy/9941009)
下载需要1积分，申请帐号后做点小任务吧。
2. 引入jquery和cookie插件。
要先引入jQuery的库文件，和 jquery.cookie.js 的库文件。 需要注意的是：JQuery必须先行引入，而后才是cookie文件，反正则错误。

来看一个例子：
```
<html>  
<head>  
<meta charset="UTF-8">  
<title>js中字符串处理</title>  
</head>  
<script type="text/javascript" src="js/jquery-1.8.0.min.js"></script>  
<script type="text/javascript" src="js/jquery.cookie.js"></script>  
<script type="text/javascript">  

    function newCookieFunc(){  
        $.cookie('cookieId',"201211011",{expires:2,path: '/'});  
        $.cookie('cookieName',"linzhiqiang",{expires:2,path: '/'});  
        alert("新建cookie成功，值分别为：cookieId：201211011  cookieName：linzhiqiang");  
    };  
    function getCookieFunc(){  
        var cookieId=$.cookie('cookieId');  
        var cookieName=$.cookie('cookieName');  
        alert("cookie的值分别为：cookieId："+cookieId+"  cookieName："+cookieName);  
    };  
    function deleteCookieFunc(){  
        $.cookie('cookieId',null,{expires:-1,path: '/'});  
        $.cookie('cookieName',null,{expires: -1,path: '/'});  
        alert("删除cookie成功");  
    };  
</script>  

<body>  
    <input type="button" onclick="newCookieFunc();" value="利用JQuery新建cookie信息"></br>  
    <input type="button" onclick="getCookieFunc();" value="利用JQuery读取cookie信息"></br>  
    <input type="button" onclick="deleteCookieFunc();" value="利用JQuery删除cookie信息"></br>  
</body>  
</html>  
```

## cookie参数解析
**1. expires: 365**
定义cookie的有效时间，值可以是一个数字（从创建cookie时算起，以天为单位）或一个Date 对 象。如果省略，那么创建的cookie是会话cookie，将在用户退出浏览器时被删除。
**2. path: '/'**
默认情况：只有设置cookie的网页才能读取该cookie。 定义cookie的有效路径。默认情况下，该参数的值为创建 cookie 的网页所在路径（标准浏览器的行为）。如果你想在整个网站中访问这个cookie需要这样设置有效路径：path: '/'。如果你想删除一个定义 了有效路径的 cookie，你需要在调用函数时包含这个路径:$.cookie('the_cookie', null, { path: '/' });。 domain: 'example.com' 默认值：创建 cookie的网页所拥有的域名。
**3. secure: true**
默认值：false。如果为true，cookie的传输需要使用安全协议（HTTPS）。
**4. raw: true**
默认值：false。 默认情况下，读取和写入 cookie 的时候自动进行编码和解码（使用encodeURIComponent 编码， decodeURIComponent 解码）。要关闭这个功能设置 raw: true 即可。

[参考文章——CSDN](http://blog.csdn.net/linzhiqiang0316/article/details/52032641)
