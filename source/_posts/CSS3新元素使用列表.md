---
title: CSS3新元素使用列表
date: 2017-10-20 00:01:12
categories: "前端"
tags:
     - CSS3
description:
---

> 最近想做一些UI组件，稍微复习一下CSS3的内容。
<!--more-->

### 边框
border-radius
box-shadow
```
box-shadow: 10px 10px 5px #888888;
```
border-image
```
-webkit-border-image: url(border.png) 30 round; /* Safari 3.1-5 */
-o-border-image: url(border.png) 30 round; /* Opera 11-12.1 */
border-image: url(border.png) 30 round;

```
### 圆角
border-radius

### 背景
background-image
background-size
background-origin
```
background-size:100% 100%;
background-origin:content-box;
```
background-clip
```
background-clip: content-box;
```

### 渐变（Gradients）
[传送门](http://www.runoob.com/css3/css3-gradients.html)

### 文本效果
text-shadow
```
text-shadow: 5px 5px 5px #FF0000;
```
box-shadow
```
box-shadow: 10px 10px grey;
```
text-overflow
```
text-overflow:ellipsis;
```
word-wrap
```
word-wrap:break-word;
```
word-break
```
word-break:keep-all;
word-break:break-all;
```

### @font-face 规则
```
@font-face
{
    font-family: myFirstFont;
    src: url(sansation_bold.woff);
    font-weight:bold;
}
```
### 2D 转换
translate()
```
transform: translate(50px,100px);
-ms-transform: translate(50px,100px); /* IE 9 */
-webkit-transform: translate(50px,100px); /* Safari and Chrome */
```
rotate()
```
transform: rotate(30deg);
-ms-transform: rotate(30deg); /* IE 9 */
-webkit-transform: rotate(30deg); /* Safari and Chrome */
```
scale()
```
-ms-transform:scale(2,3); /* IE 9 */
-webkit-transform: scale(2,3); /* Safari */
transform: scale(2,3); /* 标准语法 */
```
skew()
```
transform: skew(30deg,20deg);
-ms-transform: skew(30deg,20deg); /* IE 9 */
-webkit-transform: skew(30deg,20deg); /* Safari and Chrome */
```
matrix()
```
transform:matrix(0.866,0.5,-0.5,0.866,0,0);
-ms-transform:matrix(0.866,0.5,-0.5,0.866,0,0); /* IE 9 */
-webkit-transform:matrix(0.866,0.5,-0.5,0.866,0,0); /* Safari and Chrome */
```

### 3D方法
rotateX()
```
transform: rotateX(120deg);
-webkit-transform: rotateX(120deg); /* Safari 与 Chrome */
```
rotateY()

### 过渡
```
transition: width 2s, height 2s, transform 2s;
-webkit-transition: width 2s, height 2s, -webkit-transform 2s;
```
所有属性
```
transition-property: width;
transition-duration: 1s;
transition-timing-function: linear;
transition-delay: 2s;
/* Safari */
-webkit-transition-property:width;
-webkit-transition-duration:1s;
-webkit-transition-timing-function:linear;
-webkit-transition-delay:2s;
```

### @keyframes 规则
动画
```
// 应用
div
{
    animation: myfirst 5s linear 2s infinite alternate;
    /* Safari 与 Chrome: */
    -webkit-animation: myfirst 5s linear 2s infinite alternate;
}
// 简写
@keyframes myfirst
{
    from {background: red;}
    to {background: yellow;}
}
@-webkit-keyframes myfirst /* Safari 与 Chrome */
{
    from {background: red;}
    to {background: yellow;}
}
// 详细
@keyframes myfirst
{
    0%   {background: red; left:0px; top:0px;}
    25%  {background: yellow; left:200px; top:0px;}
    50%  {background: blue; left:200px; top:200px;}
    75%  {background: green; left:0px; top:200px;}
    100% {background: red; left:0px; top:0px;}
}

@-webkit-keyframes myfirst /* Safari 与 Chrome */
{
    0%   {background: red; left:0px; top:0px;}
    25%  {background: yellow; left:200px; top:0px;}
    50%  {background: blue; left:200px; top:200px;}
    75%  {background: green; left:0px; top:200px;}
    100% {background: red; left:0px; top:0px;}
}
```

### 多列
column-count

column-gap

column-rule-style

column-rule-width

column-rule-color

column-rule

column-span

column-width

### 用户界面
resize
```
resize:both;
```
box-sizing
```
box-sizing:border-box;
-moz-box-sizing:border-box; /* Firefox */
```
outline-offset
```
outline-offset:10px;
```

### 弹性盒子(Flex Box)
[传送门](http://www.runoob.com/css3/css3-flexbox.html)

### 媒体查询
```
@media screen and (min-width: 480px) {
    body {
        background-color: lightgreen;
    }
}
```
