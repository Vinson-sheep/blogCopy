---
title: CSS3中user-select的使用
date: 2017-10-22 15:25:33
categories: "前端"
tags:
     - CSS
     - CSS3
description: no
---

## 语法：
user-select：none | text | all | element
```
默认值：text
适用于：除替换元素外的所有元素
继承性：无
动画性：否
计算值：指定值
```
## 取值：
```
none：
文本不能被选择
text：
可以选择文本
all：
当所有内容作为一个整体时可以被选择。如果双击或者在上下文上点击子元素，那么被选择的部分将是以该子元素向上回溯的最高祖先元素。
element：
可以选择文本，但选择范围受元素边界的约束
```

## 说明：
设置或检索是否允许用户选中文本。

IE6-9不支持该属性，但支持使用标签属性 onselectstart="return false;" 来达到 user-select:none 的效果；Safari和Chrome也支持该标签属性；

直到Opera12.5仍然不支持该属性，但和IE6-9一样，也支持使用私有的标签属性 unselectable="on" 来达到 user-select:none 的效果；unselectable 的另一个值是 off；

除Chrome和Safari外，在其它浏览器中，如果将文本设置为 -ms-user-select:none;，则用户将无法在该文本块中开始选择文本。不过，如果用户在页面的其他区域开始选择文本，则用户仍然可以继续选择将文本设置为 -ms-user-select:none; 的区域文本；

对应的脚本特性为userSelect。

## 实例：
```
<!DOCTYPE html>
<html lang="zh-cmn-Hans">
<head>
<meta charset="utf-8" />
<title>user-select_CSS参考手册_web前端开发参考手册系列</title>
<meta name="author" content="Joy Du(飘零雾雨), dooyoe@gmail.com, www.doyoe.com" />
<meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1" />
<style>
.test{padding:10px;-webkit-user-select:none;-moz-user-select:none;-o-user-select:none;user-select:none;background:#eee;}
</style>
</head>
<body>
<div class="test" onselectstart="return false;" unselectable="on">选择我试试，你会发现怎么也选择不到我，哈哈哈哈</div>
</body>
</html>
```

传说门
[user-select](http://www.css88.com/book/css/properties/user-interface/user-select.htm)
