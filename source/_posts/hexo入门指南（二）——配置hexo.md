---
title: hexo入门指南（二）——配置hexo
date: 2017-09-20 20:25:24
categories: "博客建设"
tags:
     - Hexo教程
     - github
description: hexo配置文件的修改
---

按照上一篇文章，通过github pages可以访问你的博客。如果要做更个性化的设定，首先要修改hexo的项目配置文件_config.yml
<!--more-->
---

## 配置文件的详细信息。
文件内容可能有差异，但是基本的东西还是不变的。

```
# Site #站点信息
title: blog Name #标题
subtitle: Subtitle #副标题
description: my blog desc #描述
author: me #作者
language: zh-CN #语言
timezone: Asia/Shanghai #时区

# URL
url: http://yoururl.com   #用于绑定域名, 其他的不需要配置
root: /
#permalink: :year/:month/:day/:title/
permalink: posts/title.html
permalink_defaults:

# Directory #目录
source_dir: source #源文件
public_dir: public #生成的网页文件
tag_dir: tags #标签
archive_dir: archives #归档
category_dir: categories #分类
code_dir: downloads/code
i18n_dir: :lang #国际化
skip_render:

# Writing #写作
new_post_name: :title.md #新文章标题
default_layout: post #默认模板(post page photo draft)
titlecase: false #标题转换成大写
external_link: true #新标签页里打开连接
filename_case: 0
render_drafts: false
post_asset_folder: false
relative_link: false
future: true
highlight: #语法高亮
  enable: true
  line_number: true #显示行号
  auto_detect: true
  tab_replace:

# Category & Tag #分类和标签
default_category: uncategorized #默认分类
category_map:
tag_map:

# Date / Time format #日期时间格式
## http://momentjs.com/docs/#/displaying/format/
date_format: YYYY-MM-DD
time_format: HH:mm:ss

# Pagination #分页
per_page: 10 #每页文章数, 设置成 0 禁用分页
pagination_dir: page

# Extensions #插件和主题
## 插件: http://hexo.io/plugins/
## 主题: http://hexo.io/themes/
theme: next

# Deployment #部署, 同时发布在 GitHub 和 GitCafe 上面
deploy:
- type: git
  repo: git@gitcafe.com:username/username.git,gitcafe-pages
- type: git
  repo: git@github.com:username/username.github.io.git,master

# Disqus #Disqus评论系统
disqus_shortname:

plugins: #插件，例如生成 RSS 和站点地图的
- hexo-generator-feed
- hexo-generator-sitemap

```

[参考资料](http://www.jianshu.com/p/b7886271e21a)
