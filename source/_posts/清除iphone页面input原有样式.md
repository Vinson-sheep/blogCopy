---
title: 清除iphone页面input原有样式
date: 2017-09-22 22:28:20
categories: "前端"
tags:
     - CSS
description:
---

> 我在做网站的时候遇到过这样的问题: 自己手机预览的页面跟其他手机的不一样。最初以为是手机浏览器问题，跑了一下acid，性能评分100，瞬间就蒙了。考虑到浏览器本身漏洞没有被测出来，用wechat测试了一下页面，预览结果还是不符合预期。最后，发现是iphone自身样式所致。

如果没有给页面的input和textarea设定详细的css样式，iphone显示的页面效果很可能跟自己在chrome上的有出入。原因是iphone页面显示有自带样式，，比如iphone的input圆角半径会较一般浏览器大，可能是内核问题（欢迎补充）。所以编写CSS的时候不要依赖调试浏览器中显示的样式，尽可能地给input设置详细的样式，当然，也可以使用一下代码：

```
input[type="text"],
input[type="button"],
input[type="submit"],
input[type="reset"] {
-webkit-appearance: none;}
textarea {-webkit-appearance: none;}
```

[参考资料——CSDN](http://blog.csdn.net/liyuedan/article/details/42487347)
