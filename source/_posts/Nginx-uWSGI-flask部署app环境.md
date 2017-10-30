---
title: Nginx+uWSGI+flask部署app环境
date: 2017-09-21 23:09:24
categories: "服务器部署"
tags:
     - Nginx
     - uWSGI
     - flask
     - mysql
description: 利用一套技术栈实现强有力的后台部署
---

想有一个响应速度快、后台稳定的服务器环境，仅靠框架（比如flask）自带服务器系统是不足够的。利用Nginx和uWSGI,实现强有力的服务器环境，可以让页面相应速度上升几十倍。
<!--more-->

> 以前用过纯JS写过一个博客，但是毕竟自己研究前端比较多，对于后台配置不太熟悉。当时使用了flask做后台框架，由于flask自带服务器系统，所以平时就开flask服务器就算了。后来发现，flask自带的服务器非常不稳。由于社团项目需要，通过同学的推荐，我决定使用这么一套技术栈搭建后台。
Ubuntu 14.04.05 + mysql + uWSGI + python3 + git

## 安装mysql
1. 终端安装mysql
```
sudo apt-get install mysql-server
sudo apt-get install mysql-client
sudo apt-get install libmysqlclient-dev
# 用下面语句检查是否安装成功
sudo netstat -tap | grep mysql
```
2. 安装mysql时会有一个用户名`debian-sys-maint`和一个随机密码。
```
sudo vi /etc/mysql/debian.cnf
```
3. 找到帐号密码然后登录mysql命令行
```
mysql -u debian-sys-maint -p
```
4. 进入控制台后，修改密码
```
use mysql;
update user set password=PASSWORD('新密码') where user='root'; FLUSH PRIVILEGES;
```
5. 输入`quit`退出控制台。

## python3安装
1. 终端安装python3
```
sudo apt-get install python3
```
2. 安装pip3
```
sudo apt-get install python3-pip
```
3. 顺便安装pip
```
sudo apt-get install python-pip
```
4. 再把mysql的python驱动装了吧
```
sudo pip3 install mysqlclient
```

## 安装git
```
sudo apt-get install git
```

## 配置代码运行的环境
Python的虚拟环境，可以隔离各个项目，避免python版本冲突
```
sudo pip3 install virtualenv
```
假设我的项目目录是`/home/jnugeek`，进入根目录，执行
```
virtualenv jnugeek
source jnugeek/bin/activate #进入虚拟环境
```
这样就创建了名为`jnugeek`的虚拟环境，
直接在后台输入`deactivate`退出虚拟环境

## uWSGI配置
uWSGI是高性能http服务器，用来和Python程序交换
```
(jnugeek)jnugeek root$ pip3 install uwsgi
```
在虚拟环境下不需要使用`sudo`，因为virtualenv 是没有权限要求的。
在项目目录下创建`config.ini`作为uWSGI的配置文件
```
[uwsgi]
master = true
home = jnugeek #虚拟环境文件夹
wsgi-file = manage.py
callable = app
socket = :5000
processes = 4
threads = 2
buffer-size = 32768
```
(虚拟环境内)运行文件
```
uwsgi config.ini
```
如果没有报错的话就是可以的，但是会有一些比较坑爹的错误
```
!!! no internal routing support, rebuild with pcre support !!!
```
这个是因为pcre没弄好，一般去掉缓存重装就可以了，-I的作用是重装
```
pip3 install uwsgi -I --no-cache-dir
```

## 安装Flask
在根目录下新建一个requirements.txt文件，输入
```
Flask==0.10.1
Flask-Login==0.2.11
Flask-Mail==0.9.1
Flask-Moment==0.4.0
Flask-PageDown==0.1.5
Flask-SQLAlchemy==2.0
Flask-Script==2.0.5
Flask-WTF==0.10.2
Flask-Cache==0.13.1
Flask-Restless==0.15.0
Flask-Uploads==0.1.3
Jinja2==2.7.3
Mako==1.0.0
Markdown==2.5.1
MarkupSafe==0.23
SQLAlchemy==0.9.8
WTForms==2.0.1
Werkzeug==0.9.6
html5lib==1.0b3
itsdangerous==0.24
six==1.8.0
awesome-slugify==1.6
```
安装清单文件
```
(jnugeek)jnugeek root$ pip3 install -r requirements.txt
```

## supervisor配置
uWSGI好是好，但是要是它万一断了，或者出问题了怎么办？要是有这样的一个程序可以自动监控运行uWSGI那岂不是美滋滋，而supervisor就是这样的程序。
安装
```
sudo apt-get install supervisor
```
在/etc/supervisor/conf.d/下建立一个配置文件sp.conf
```
[program:my_flask]
# 启动命令入口
command=/home/jnugeek/jnugeek/bin/uwsgi /home/jnugeek/config.ini
# 命令程序所在目录
directory=/home/jnugeek
#运行命令的用户名
user=root
autostart=true
autorestart=true
#日志地址（需要手动新建文件）
stdout_logfile=/home/jnugeek/logs/uwsgi_supervisor.log
```
启动/重启/查看状态命令
```
sudo service supervisor start/restart/stats
```

## 安装Nginx
```
sudo apt-get install nginx
```
新建一个default文件（无后缀）
```
server {
  listen 80;
  server_name X.X.X.X; #公网地址
  location / {
  include uwsgi_params;
  uwsgi_pass 127.0.0.1:5000; # 指向uwsgi 所应用的内部地址,所有请求将转发给uwsgi 处理
  uwsgi_param UWSGI_PYHOME /home/jnugeek/jnugeek; # 指向虚拟环境目录
  uwsgi_param UWSGI_CHDIR /home/jnugeek; # 指向网站根目录
  uwsgi_param UWSGI_SCRIPT manage:app; # 指定启动程序
  uwsgi_read_timeout 100;
 }  
}
```

测试一下配置是否正确
```
sudo nginx -t
```
将/etc/nginx/sites-available/default替换掉
```
sudo service nginx restart
```
将你的项目文件装载后，在浏览器中输入你的IP地址，就可以看到你的项目了。

在哪里查看错误日志呢？
> /var/log/nginx/error.log

[参考资料1——简书](http://www.jianshu.com/p/84978157c785)
[参考资料2——博客园](http://www.cnblogs.com/Ray-liang/p/4173923.html)
[参考资料3——同学的博客](https://blog.patrickcty.cc/2017/03/02/%E5%86%8D%E6%AC%A1%E9%83%A8%E7%BD%B2Flask-app/)
