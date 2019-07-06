---
layout: post
title: 在Docker中使用Flask进行WEB开发-1
date: 2019-07-03T23:37:28+03:00
comments: true
published: true
categories: [python]
tags: [python, flask, docker]
---

## 序言

记得最早接触的编程语言有Visual Basic，C#，以及Java，这些语言在工作之后就都再也没有用过了。当然不是说这些语言不好，比如说Java，那是常年位居第二的编程语言。只是说没有了那样一个好的应用场景存在，就没有机会认真去学习了。

之后偶然的机会，也是因为当时（2010年左右）Wordpress的盛行，开始学习PHP语言。再往后逐渐了解到Joomla，Drupal，Codeigniter等用PHP语言开发的WEB开发框架，并开始以此为基础，尝试做各种小项目的二次开发。

再后来，又是偶然的机会，也是因为当时（2014年前后）Bitcoin以及其他各种数字货币的盛行，开始接触并学习Golang语言，并与朋友一起创建了数字货币打赏及社交分享平台: **币推**，主理前端WEB开发。

了解并学习Ruby语言以及Ruby on Rails框架，并没什么特别的原因，但是却也受益匪浅。从2016年开始，也使用这个框架搭建过一两个提高工作效率的工具类网站。

最近，又开始了新一轮的折腾，学习起Python语言来。主要动力来源于几个YouTube视频里面关于python的pandas跟numpy库的介绍，发现这个语言里面的好些库都相当强大，不免想了解更多一些。语言本身就不做过多介绍，相对更强大的框架Django也不做过多介绍。下面我们主要来谈谈，如何创建Docker环境，并使用Flask框架来做二次开发，搭建Web Application。

## 关于Docker

Docker的主要功能在于利用操作系统虚拟化，提供各自独立的单个软件开发容器，使其他软件在其中运行。它进一步推进了虚拟机的发展。简单来说，没有Docker之前，使用虚拟机进行开发，只能创建出一个虚拟机，然后再在这唯一的一个虚拟机上面安装其他各种应用程序（Python，Postgresql，Redis..），然后进行开发。这种方式的缺点在于单个虚拟机本身的负载会比较大，而且最后程序本身也会变得极其笨重。使用Docker之后，可以给各个应用程序创建不同的容器，使其各自分开运行，这样，容器跟程序都会比较轻量化。

## 关于Flask

Flask则是一个用Python语言编写出来轻量级的Web开发框架。相比较Django来说，Flask不需要特别的工具或者库就可以运行。怎么实现数据库连接，怎么实现表单验证，这些都可以自由选择。

### Flask入门

使用`brew`安装Python版本管理组件：`pyenv`

```shell
brew update
brew install pyenv
```

使用`pyenv`安装python最新稳定版本：`3.7.3`，并设置此版本为全局默认版本

```shell
pyenv install -v 3.7.3
pyenv global 3.7.3
```

使用`pip`安装`flask`库

```shell
pip install flask
```

最后创建一个python文件`index.py`，填入以下内容，并保存:

```python
from flask import Flask

app = Flask(__name__)

@app.route('/')
def index:
  return 'Hello World'
```

打开Terminal，`cd`转至`index.py`所在文件夹，之后运行以下command：

```shell
export FLASK_APP=index.py
export FLASK_ENV=development # 可选(Optional)
export FLASK_DEBUG=1 # 可选(Optional)
flask run
```

打开浏览器，转至`http://localhost:4000`，*Hello World*文字显示在浏览器中，即表示运行成功。
