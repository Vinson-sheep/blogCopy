---
title: hexo主题indigo——安装
date: 2017-09-21 18:52:01
categories: "博客建设"
tags:
     - Hexo教程
     - indigo
description: indigo的安装
---

本站使用的是indigo主题。这个主题UI相对比较美观，功能齐全，但是可个性化的部分比较少，图片镶嵌不足。如果想要一个更个性化的主题，我推荐material主题。
<!--more-->

> 使用indigo请先下载最新版的git和nodejs，博主曾经因为使用4.0版本的nodejs而折腾了一个下午，最终使用8.x的nodejs完美解决。
文章的内容都来自文章末尾的文档链接，想要更详细的可以直接去看文档。

## 主题安装
安装需确认你的 Hexo 版本在 3.0 以上，以及 Node 版本为 6.x 以上，在 Hexo 根目录，执行以下命令。
```
git clone git@github.com:yscoder/hexo-theme-indigo.git themes/indigo
```

## 依赖安装
还是在 Hexo 根目录，如果以下插件已安装过，无需再次安装。
### Less
主题默认使用 less 作为 css 预处理工具。
```
$ npm install hexo-renderer-less --save
```

### Feed
用于生成 rss。
```
$ npm install hexo-generator-feed --save
```

### Json-content
用于生成静态站点数据，用作站内搜索的数据源。
```
$ npm install hexo-generator-json-content --save
```

### QRCode
用于生成微信分享二维码。
> 可选，不安装时会请求 jiathis Api 生成二维码。

```
$ npm install hexo-helper-qrcode --save
```

## 修改hexo配置文件
用文本编辑器（建议不要用win自带的文本编辑器）打开_config.yml，修改
`theme: indigo`

配置完成，在git bash输入`hexo s`预览主题。



[hexo主题列表](https://github.com/hexojs/hexo/wiki/Themes)
[浏览更多主题](https://hexo.io/themes/)
[indigo主题文档传送门](https://github.com/yscoder/hexo-theme-indigo/wiki)
