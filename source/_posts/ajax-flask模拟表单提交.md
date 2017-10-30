---
title: ajax+flask模拟表单提交
date: 2017-09-22 22:30:58
categories: "前端"
tags:
     - Ajax
     - flask
     - 表单
description:
---

> 首先，当前端页面存在表单时，默认的commit往往不符合预期。即使页面html中存在表单验证功能，效果甚微。而commit之后不管三七二十一直接跳转到另一个页面，如果这符合你预期固然好，不过我一般还是用xhr(XMLHttpRequest)定制自己commit的事件
<!--more-->

## 前端
### 首先取得commit的按钮节点
```
btn = form['commit-btn'];
```
### 取消默认行为
```
btn.onclick = function(e) {
    e.preventDefault();
    submit_btn.disabled = true; //禁用commit按钮
    //表单验证
    //数据处理
    //xhr模拟提交
    //相应后的操作
}
```
这里需要注意一下。`return false`也是可以阻止默认行为，但我们一般还需要表单验证，直接就return自然不符合我们的预期。禁用commit按钮是为了避免重复提交表单，需要启用按钮就改为`=false`就可以。

### 数据处理
```
// 基本格式
name = '丽江';
text = 'abc';
name = encodeURIComponent(name);
text = encodeURIComponent(text);
data = 'name=' + name + '&' + 'text=' + text;
//name=%E4%B8%BD%E6%B1%9F&text=abc
```

### xhr模拟表单提交
```
xhr = new XMLHttpRequest();
url = '/abc'; //自行修改地址
xhr.open("post", url,false); //同步提交为false，异步可以用true
xhr.setRequestHeader("Content-Type","application/x-www-form-urlencoded");//模拟表单需要修改header
xhr.send(data);//传输数据
```
### 获取相应后再操作页面
```
if ((xhr.status >= 200 && xhr.status <300) || xhr.status == 304 ) {
            submit_btn.disabled = false;
            //刷新页面
            location.reload();
        } else {
            alert('评论失败，请检查你的网络');
            submit_btn.disabled = false;
        }
```
提交失败后不要忘记将submit_btn开启`(设置disable = false)`

## 后台
### 假设你有一个app.py
```
from flask import Flask,request
import urllib
from urllib import parse

app = Flask(__name__)

@app.route('/abc',methods=['POST'])
def comment_write(html_src):
    #一顿操作
    pass


if __name__ == '__main__':
    app.run(host='0.0.0.0',port=80) //外网访问，host是关键
```
### 获取表单内容
```
name = urllib.parse.unquote(request.form['name']) #丽江
text = urllib.parse.unquote(request.form['text']) #abc
#unquote方法用来解析url参数
```
### 对post请求作出响应
```
return 'successful'
```
如果不做出请求响应，前台会认为响应失败，返回400状态码，相对地，相应成功会返回200和304，部分浏览器会返回204响应码。

## 总结
ajax模拟表单提交实际上就是取消默认操作、获取表单数据并处理、xhr发送请求、相应处理的过程。大家可能注意到，即使前台使用默认的commit提交表单，后台代码也仅仅不需要unquote而已。可以说，使用ajax提交表单跟默认提交表单，后台操作是类似的。

在数据处理方面，有值得注意的地方。data数据的格式与get方法在地址栏提交的数据格式几乎一样（就是少了个？），猜测post请求提交数据的过程与get方法提交数据的原理是相似的，只是提交方式有差异。
