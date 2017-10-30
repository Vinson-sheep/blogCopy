---
title: hexo入门指南（四）——文章模版
date: 2017-09-20 20:27:00
categories: "博客建设"
tags:
     - Hexo教程
     - github
description: 写文章的时候要注意
---

一般我是记不住文章开头要写些什么关键内容，所以我就做个文章模版，待我写文章的时候就能做参考。
<!--more-->

## 新建页面
在git bash中输入
`hexo new "your file name"`
在路径\blog\source\_posts中会生成一个md文件

## 文章模版
要注意hexo文章使用的是markdown语法，建议不要去尝试其他文本格式(虽然亲测html是有效的)。

这里附上本文的配置
```
---
title: hexo入门指南（四）——文章模版
date: 2017-09-20 20:27:00
categories: "博客建设"
tags:
     - Hexo教程
     - github
description: 写文章的时候要注意
---

一般我是记不住文章开头要写些什么关键内容，所以我就做个文章模版，待我写文章的时候就能做参考。
<!--more-->
```

## 文章发布
1. 写文章的时候，可以在git bash中输入`hexo s`,然后保存文章后刷新页面`localhost:4000`即可看到最新的变化。
2. 想要发布文章，在git bash中输入
`hexo clean && hexo g && hexo d`
关于内联语句的含义，可以查看**入门指南（一）**

于是我们就可以轻松愉快地写文章了。
