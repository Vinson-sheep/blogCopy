---
title: jquery插件blindify详解
date: 2017-10-22 13:58:19
categories: "前端"
tags:
     - jquery
     - jquery插件
description: no
---

> 百叶窗插件，因为使用的是jquery，所以兼容大部分浏览器，ie兼容9+。
<!--more-->

## 简介
![](http://ohkgqh4gv.bkt.clouddn.com/1508652225%281%29.png)

Blindify 是一个基于 jQuery 的百叶窗幻灯片插件，它能够非常方便的制作一个漂亮的百叶窗效果，你还可以设置百叶窗的片数、间隔、宽度、高度以及各种动画效果的时间和百叶窗的方向——水平或垂直。

## 兼容
### jQuery 兼容
兼容 1.4+。
### 浏览器兼容
![](http://ohkgqh4gv.bkt.clouddn.com/1508652357%281%29.png)

## 使用方法
1、 引入文件
```
<link rel="stylesheet" href="css/blindify.min.css">
<script src="js/jquery-1.8.3.min.js"></script>
<script src="js/jquery.blindify.min.js"></script>
```
2、 HTML
```
<div id="blindify">
    <ul>
        <li><img src="images/photo_1.jpg" alt=""></li>
        <li><img src="images/photo_2.jpg" alt=""></li>
        <li><img src="images/photo_3.jpg" alt=""></li>
        <li><img src="images/photo_4.jpg" alt=""></li>
    </ul>
</div>
```
或者带有链接：
```
<div id="blindify">
    <ul>
        <li><a href="http://www.dowebok.com/"><img src="images/photo_1.jpg" alt=""></a></li>
        <li><a href="http://www.dowebok.com/"><img src="images/photo_2.jpg" alt=""></a></li>
        <li><a href="http://www.dowebok.com/"><img src="images/photo_3.jpg" alt=""></a></li>
        <li><a href="http://www.dowebok.com/"><img src="images/photo_4.jpg" alt=""></a></li>
    </ul>
</div>
```
3、JavaScript
```
$(function(){
    $('#blindify').blindify();
});
```
配置

| 属性/方法 | 类型 | 默认值 | 说明 |
| -------- | ---- | ----- | ----- |
| numberOfBlinds | 整数 | 20 | 百叶窗叶片个数 |
| slideVisibleTime | 整数 | 2000 | 每个幻灯片的停留时间，不包括动画时间，以毫秒为单位 |
| color | 字符串 | #000000 | 幻灯片背景颜色（十六进制颜色） |
| margin | 整数 | 2 | 	百叶窗之间的距离，以像素（px）为单位。注意：其实是每个百叶窗的边框，所以如果想设置距离为10px，只需设置一半5px |
| width | 整数 | 960 | 容器的宽度，应与图片的宽度一样，以像素为单位 |
| height | 整数 | 600 | 容器的高度，应与图片的宽度一样，以像素为单位 |
| gap | 整数 | 100 | 百叶窗与容器边缘的距离范围，以像素为单位 |
| animationSpeed | 整数 | 100 | 幻灯片动画过度时间 |
| delayBetweenSlides | 整数 | 500 | 每个幻灯片切换之间的间隔，以毫秒为单位 |
| hasLinks | 布尔值 | false | 是否有链接 |
| orientation | 字符串 | vertical | 百叶窗的方向，可选水平（horizontal）或垂直（vertical），默认为垂直 |
| startClosed | 布尔值 | false | 百叶窗开始时是否关闭 |
| firstOpenDelay | 整数 | 500 | startClosed 为 true 时，百叶窗延迟打开时间，单位为毫秒 |
