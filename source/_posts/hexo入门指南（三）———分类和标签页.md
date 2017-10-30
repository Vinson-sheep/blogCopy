---
title: hexo入门指南（三）———分类和标签页
date: 2017-09-20 20:26:11
categories: "博客建设"
tags:
     - Hexo教程
     - github
description: 为博客设置分页和分类
---

hexo的分页和分类功能是没有被初始化的，需要特殊的设置才能使用这两个页面。
<!--more-->

> win10 + nodejs8.5.0 + git2.14.1 + indigo主题

## 设置标签页tags
1. 在git bash中输入
```
hexo new page tags
```

2. 修改 hexo/source/tags/index.md 的元数据
```
layout: tags
comments: false
---
```

## 设置分类页categories
1. 仅 card theme 支持。
```
hexo new page categories
```

2. 修改 hexo/source/tags/index.md 的元数据
```
layout: categories
comments: false
---
```

设置了标签页和分类页后，hexo会基于你的文章信息进行分类并添加到页面上。基本上不用理会这两个页面。

[参考资料](https://github.com/yscoder/hexo-theme-indigo/wiki/%E9%85%8D%E7%BD%AE)
