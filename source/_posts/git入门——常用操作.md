---
title: git入门——常用操作
date: 2017-09-24 13:50:03
categories: "网站维护"
tags:
     - git
     - github
description:
---

> 看了一下廖雪峰的git教程，觉得要熟悉git的操作需要一段适应时间，于是我干脆在这里写一篇总结性的git常用操作集合，方便自己日后推送和维护项目。
<!--more-->

## 日常操作
```
$ git add filename #添加文件
$ git commit -m "some message" #提交文件
$ git status #查看状态
$ git diff #查看修改内容
$ git log --pretty=oneline #查看提交记录
$ git reset --hard HEAD^ #退回上一个版本
$ git reflog #查看命令历史
$ git checkout -- filename #丢弃工作区的修改
$ git reset HEAD filename #丢弃缓存区的修改
$ git rm filename #删除文件
```

## 分支的使用
```
$ git branch dev #创建分支
$ git checkout dev #切换分支
$ git checkout -b dev #创建并切换分支
$ git branch #查看分支
$ git merge dev #合并分支
$ git branch -d dev #删除分支
$ git merge --no-ff -m "some message" dev #合并的同时commit
$ git push origin master #推送master主分支
$ git push origin dev #推送dev分支
```

## 工作现场stash
```
$ git stash #存储工作现场
$ git stash list #查看工作现场
$ git stash apply #恢复工作现场
$ git stash drop #删除工作现场
$ git stash pop #恢复和删除工作现场
$ git stash apply stash@{0} #恢复指定stash
```

## 标签tag
标签可以用来管理版本号，一般标记在master分支上
```
$ git tag v1.0 #为当前分支打上标签
$ git tag #查看所有标签
$ git tag v0.9 6224937 #为指定commit打上标签
$ git tag -a v0.1 -m "version 0.1 released" 3628164 #附带信息
$ git show v0.9 #查看标签信息
$ git tag -d v0.1 #本地删除标签

$ git push origin v1.0 #远程推送标签
$ git push origin --tags #远程推送所有标签

删除远程标签
// 先从本地删除
$ git tag -d <tagname>
// 再从远程删除
$ git push origin :refs/tags/<tagname>
```

## 远程协作
```
//克隆远程仓库
$ git clone git@github.com:michaelliao/learngit.git

//创建本地dev分支
$ git checkout -b dev origin/dev

对dev修改后可以推送提交

//推送dev分支
$ git push origin dev

如果其他人已经推送了新的版本，会显示有冲突

//将其他人最新的提交抓去下来
$ git pull

但是git pull会失败，原因是没有设置链接

//建立本地分支和远程分支的关联
$ git branch --set-upstream branch-name origin/branch-name

//合并库
$ git commit -m "merge & fix hello.py"

如果有冲突，就解决掉

//再次推送到dev分支上
$ git push origin dev
```
