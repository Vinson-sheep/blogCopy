---
title: flask中file.save小坑
date: 2017-10-26 23:20:04
categories: "后端"
tags:
     - flask
description:
---

> 最近挖了文件上传的坑，刚开始就遇到了小坑，花了我很多时间去专研这个问题。
<!--more-->

[flask文档](http://docs.jinkan.org/docs/flask/patterns/fileuploads.html)上面有关上传文件的实例，我copy下来，放在本地运行。
```
import os
from flask import Flask, request, redirect, url_for
from werkzeug import secure_filename

UPLOAD_FOLDER = '/path/to/the/uploads'
ALLOWED_EXTENSIONS = set(['txt', 'pdf', 'png', 'jpg', 'jpeg', 'gif'])

app = Flask(__name__)
app.config['UPLOAD_FOLDER'] = UPLOAD_FOLDER

def allowed_file(filename):
    return '.' in filename and \
           filename.rsplit('.', 1)[1] in ALLOWED_EXTENSIONS

@app.route('/', methods=['GET', 'POST'])
def upload_file():
    if request.method == 'POST':
        file = request.files['file']
        if file and allowed_file(file.filename):
            filename = secure_filename(file.filename)
            file.save(os.path.join(app.config['UPLOAD_FOLDER'], filename))
            return redirect(url_for('uploaded_file',
                                    filename=filename))
    return '''
    <!doctype html>
    <title>Upload new File</title>
    <h1>Upload new File</h1>
    <form action="" method=post enctype=multipart/form-data>
      <p><input type=file name=file>
         <input type=submit value=Upload>
    </form>
    '''
```

结果出现`no such file or directory `之类的文字，python是很明确地说明是`save.file`函数保存文件路径出了问题。

实际上这个问题网上很多帖子，然而答案很模糊。**实际问题在于就是`file.save`只接受绝对路径。这个不管是Linux还是windows都是一样的**。


传送门：
[记录一个Flask文件上传的小坑](http://www.jianshu.com/p/2c97caaf3cf9)
