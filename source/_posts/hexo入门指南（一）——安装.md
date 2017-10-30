---
title: hexo入门指南（一）——安装
date: 2017-09-20 18:47:44
categories: "博客建设"
tags:
     - Hexo教程
     - github
description: hexo的安装和配置
---

hexo是一个非常优秀的博客建设项目，github + node.js即可打造主题多样的博客界面。本站正是利用hexo建设的博客，稍微复习一下流程。
<!--more-->

> 为什么要做自己的博客呢？可能是为了装B吧，利用hexo建设的博客可以不用花钱，只可能花掉你部分学习时间。不过我更想有一个集中自己笔记的地方，原来喜欢在简书上面打MD，后来发现还是没自己博客的B装得好，所以就搞了这个博客。

## 概述
hexo搭建博客可以分为以下几个步骤：
1. 安装node.js和git
2. github帐号申请和配置
3. 安装hexo
4. 配置hexo
5. 将hexo和github关联起来
6. hexo常用操作

## 第一步：安装node.js和git
### 安装git
1. 先从官网下载[git安装包](https://git-for-windows.github.io/)，然后一路默认安装
2. 建议直接安装最新版本（包括node.js），避免某些主题由于git和node.js版本问题而无法使用（此处是坑）
![注意选择第二个](http://ohkgqh4gv.bkt.clouddn.com/1531909-44bddccbb0bc44fb.png)
3. 安装完成后在cmd中输入`git --version`检测安装结果

### 安装node.js
1. 提供地址[点击此处](https://nodejs.org/en/)
![下载对应版本](http://ohkgqh4gv.bkt.clouddn.com/1531909-acb3ca9d69e0037f.png)
2. 下载系统的对应版本，然后一路默认安装即可。
3. 安装完成后在cmd中输入`node -v`和`npm -v`检测安装结果

## 第二步：github帐号申请和配置
>github是世界上最大的同性交友平台，emm，好吧，它是一个流行的代码托管平台。利用github pages功能，让页面在网络上跑起来。

1. [提供github官网](https://github.com/)。国内上github官网一般加载很久，解决方法请看[此处](http://www.cnblogs.com/fengnovo/p/5959880.html)
2. 申请github帐号
3. 点击`New repository`
![](http://ohkgqh4gv.bkt.clouddn.com/1505906428%281%29.png)
4. 输入Repository name为`yourname.github.io`
![](http://ohkgqh4gv.bkt.clouddn.com/1505906470%281%29.png)
5. 然后点击`Create repository`
![](http://ohkgqh4gv.bkt.clouddn.com/1505906489%281%29.png)
现在应该可以在网址栏输入`yourname.github.io`查看你的github page（然而什么都没有）。

## 第三步：安装hexo
1. 在磁盘合适的地方建一个文件夹，本文的路径是E:/blog
2. 在文件夹内右键，点击git bash
3. 在国内利用npm命令容易被墙，利用淘宝镜像可以轻松解决,之后的安装都用`cnpm`代替`npm`。
`$ npm install -g cnpm --registry=https://registry.npm.taobao.org`
4. 利用npm命令安装hexo
`cnpm install -g hexo-cli`
`cnpm install hexo --save`
验证是否安装正确
`hexo -v`

5. 本地运行hexo
`hexo init`
![这时候会有报错,这时候只要按照报错提示操作即可](http://ohkgqh4gv.bkt.clouddn.com/1505628920%281%29.png)
如图执行`cnpm install`
6. hexo安装完成。可在git bash输入`hexo -v`验证是否安装正确。

## 第四步：配置hexo
### 安装主题
1. 利用git命令克隆主题文件（以主题next为例）
`git clone https://github.com/iissnan/hexo-theme-next themes/next`
这里themes/next是安装路径，http..next是github地址。
2. [更多主题浏览这里](https://hexo.io/themes/)

### 修改配置文件
1. 打开根目录下的_config.yml
![](http://ohkgqh4gv.bkt.clouddn.com/1505908686%281%29.png)
2. 修改基本配置
![](http://ohkgqh4gv.bkt.clouddn.com/1531909-cd5743eda172deca.png)
3. 修改主题
将theme栏的值改为`next`即可
4. 测试你的网站
在git bash中输入`hexo g && hexo s`。打开浏览器，在地址栏输入`localhost:4000`，查看你的页面。正常情况下，你的页面已经在本地跑起来了。

## 第五步：将hexo和github关联起来
1. 再次打开根目录下的_config.yml，修改配置。
![](http://ohkgqh4gv.bkt.clouddn.com/1531909-d0fc558c749b5569.png)
2. 安装hexo-deployer-git自动部署发布工具
`cnpm install hexo-deployer-git  --save`
3. 发布到github上
`hexo clean && hexo g && hexo d`
第一次发布要求输入你的github帐号密码，可能会比较慢。
4. 访问测试。
发布完毕后在浏览器中输入`https://yourname.github.io/`

## 第六步：hexo常用操作
```
hexo new page "page" #新建页面
hexo new "article" #新建文章
hexo g #生成
hexo s #启动服务预览
hexo d #部署
```
[更多hexo操作请看这里](https://segmentfault.com/a/1190000002632530)

[参考资料](http://www.jianshu.com/p/189fd945f38f)

[参考资料1](http://blog.csdn.net/gdutxiaoxu/article/details/53576018)
