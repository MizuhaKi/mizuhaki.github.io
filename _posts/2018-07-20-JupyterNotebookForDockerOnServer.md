---
layout: post
title: Jupyter Notebook In Docker for Server
author: Mizuha Ki
date: 2018-07-20
categories:
- computer science
- deep learning
- jupyter notebook
tags:
- computer science
- deep learning
- jupyter notebook
- blog
---

## 生成jupyter配置文件，这个会生成配置文件.~/.jupyter/jupyter_notebook_config.py
```bash
jupyter notebook --allow-root --generate-config
```

## 使用ipython生成密码
```bash
In [1]: from notebook.auth import passwd
In [2]: passwd()
Enter password: 
Verify password: 
Out[2]: 'sha1:XXX'
```


## 去配置文件.~/.jupyter/jupyter_notebook_config.py中修改以下参数
```bash
c.NotebookApp.ip='*'                          #绑定所有地址
c.NotebookApp.password = u'sha1:XXX'
c.NotebookApp.open_browser = False            #启动后是否在浏览器中自动打开

c.NotebookApp.port = 8888                      #指定一个访问端口，默认8888，注意和映射的docker端口对应

start jupyter notebook --allow-root
```

## 浏览器打开
https://xxx.xxx.xxx.xxx:8888/
