---
title: hexo主题indigo——配置
date: 2017-09-21 18:52:28
categories: "博客建设"
tags:
     - Hexo教程
     - indigo
description: indigo配置文件的修改
---

修改indigo可以个性化你的页面。由于indigo使用的是utf-8编码，不用担心中英文输入问题。图片的替换只需更好图片内容或者路径即可，相当简单。
<!--more-->

> 无论是主题的安装还是配置，千万千万要看它的文档。（文档链接在末尾）

## 站点配置
编辑站点配置文件，**hexo/_config.yml**。

### 启用主题
```
theme: indigo
```

### 基本配置
为了得到更好的使用体验，以下内容请务必填写完整，因为这些内容会在主题中得到展示。
```
title: your title
subtitle: your subtitle
description: your description
keywords: your keywords
author: your name
email: your email
url: your site url
```

## 主题配置

编辑主题配置文件，**themes/indigo/_config.yml**。

##左侧菜单
默认配置如下
```
menu:
  home:
    text: 主页
    url: /
  archives:
    url: /archives
  tags:
    url: /tags
  github:
    url: https://github.com/yscoder
    target: _blank
  weibo:
    url: http://www.weibo.com/ysweb
    target: _blank
  link:
    text: 测试
    url: /
```
添加新菜单项时，在 menu 下增加子属性即可。属性说明如下：
```
menu:
 link:               # fontawesome图标，省略前缀，本主题前缀为 icon-，必须
   text: About       # 菜单显示的文字，如果省略即默认与图标一致，首字母会转大写
   url: /about       # 链接，绝对或相对路径，必须
   target: _blank    # 是否跳出，省略则在当前页面打开
```
fontawesome 图标已集成到主题中，你可以到[这个页面](http://fontawesome.io/icons/)挑选合适的图标。

## favicon
站点 logo，显示在浏览器当前标签页左上角。
```
favicon: /favicon.ico
```

## 头像
位于左侧菜单上方
```
avatar: /img/logo.jpg
```

## email
头像下方
```
email: 634206017@qq.com
```

## color
设置 Android L Chrome 浏览器状态栏颜色，不需要可去除此项或设为 false。
```
color: '#3F51B5'
```

## 页面标题 (card theme)
自定义归档、标签、分类页的大标题。
```
tags_title: Tags
archives_title: Archives
categories_title: Categories
```

## 文章摘要
可以在 Markdown 文件中加 <!--more-->以分割摘要与文章正文。未设置时，按 excerpt_length 设置截取。
```
# 文章摘要渲染方式: 为 true 时将渲染为 html，否则为文本
excerpt_render: false
# 截断长度
excerpt_length: 200
# 文字正文页链接文字
excerpt_link: 阅读全文...
```

## 分享
文章分享开关，by[jiathis-api](http://www.jiathis.com/help/html/share-with-jiathis-api)。
```
share: true
```

## 文章打赏
默认开启
```
reward:
  title: 谢谢大爷~             #显示的文字
  wechat: /img/wechat.jpg     #微信，关闭设为 false
  alipay: /img/alipay.jpg     #支付宝，关闭设为 false
```
此外在 crad theme 中，可以通过在 markdown 头部添加 reward: false 来控制某些不想开启打赏的页面。

关闭
```
reward: false
```
> 二维码请自行从微信、支付宝中下载。当两个二维码同时存在时，为保持显示效果的一致性，注意截图时的边框留白保持一致。必要时可借助PS等图片处理工具进行图片大小裁剪、压缩等。

## 站内搜索
是否开启搜索
```
search: true
```

## 布局
开启后，文章页在大屏下会隐藏左侧菜单，专注阅读。
```
hideMenu: true
```

## Toc
开启文章内容导航。
```
#toc: false  #关闭
toc:
  list_number: false  # 决定导航使用的标签， true 为 ol， false 为 ul。
```

## copyright (card theme)
文章页版权声明内容，hexo中所有变量及辅助函数等均可调用，具体请查阅 hexo.io。
```
copyright: 这里写留言或版权声明
```

## less
设置 less 编译时的入口文件路径，hexo-renderer-less。
```
less:
  compress: true    # 是否压缩css
  paths:
    - source/css/style.less
```

## 评论
集成了多说和 disqus，开启其一即可。
> duoshuo-key 即多说创建站点时的二级域名。如：abc.duoshuo.com，就填 abc。

```
duoshuo: duoshuo-key
```

或

```
disqus_shortname: disqus_shortname
```

## 版权起始年份
```
since_year: 2006
```

## 自定义页面关于
用户页面中作者相关的描述性文字，如不需要设为 false
```
about: 用户页面中作者相关的描述性文字，如不需要设为 false
```

[indigo主题配置文档](https://github.com/yscoder/hexo-theme-indigo/wiki/%E9%85%8D%E7%BD%AE)
