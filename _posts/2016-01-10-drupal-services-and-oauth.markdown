---
layout: post
title: Drupal服务模块
date: 2016-01-10 09:21
comments: true
categories: [php, drupal]
---

# 序

公司有个项目是基于Drupal框架搭建的，最近新的需求里面要求外部程序能够利用该项目里的功能资源。很显然，需要构造并允许RESTful API请求。Drupal开源项目里的Services模块能够很好地实现这一需求。

# 文

## Services模块

> A standardized solution for building API's so that external clients can communicate with Drupal. Out of the box it aims to support anything Drupal Core supports and provides a code level API for other modules to expose their features and functionality. It provide Drupal plugins that allow others to create their own authentication mechanisms, request formats, and response formats.

> Currently all development is happening on github for the useful help of PR's. [https://github.com/kylebrowning/services](https://github.com/kylebrowning/services)

[Drupal Services](https://www.drupal.org/project/services) 模块是为了构造API进而让外部用户能跟Drupal交流通信而产生的标准化解决方案。所有Drupal内核支持的，它也支持。它提供了一个代码层的API，从而使得其他模块能够专注于自己的功能特性。它同时还提供了Drupal插件接口，使得其他开发者能创建自己的授权机制，请求参数格式，以及返回参数格式等。

## 安装

Drupal Services模块依赖于ctools模块，所以在安装Services模块之前需要先安装ctools模块。为了使用Services模块里的Rest Server，还需要先安装Libraries模块以满足依赖。完成这四个模块的安装并启用，下一步我们可以开始配置Services端点了。

## 配置 - 利用默认资源

此处仅限于讨论怎么在不直接登录访问的情况下，获取到Drupal站点的node信息。

在浏览器里访问
`http://localhost/drupal-test/admin/structure/services/list`， 添加一个新的端点。

![添加端点](/assets/images/add_endpoint.png)

添加完成之后，可以根据需要修改参数。比如server配置，我只希望通过JSON传递数据。

![配置server](/assets/images/config_server.png)

授权机制暂时先留白。

在下一个tab里面，勾选node作为目前可用的资源，保存并继续。

![配置resource](/assets/images/add_node_resource.png)

这个时候，可以使用Postman来测试API是否构造成功。

### 1. 获取所有node：

#### 请求：

```sh
GET /drupal-test/api/books/node HTTP/1.1
Host: localhost
Cache-Control: no-cache
```

#### 返回：

```json
[
    {
        "nid": "4",
        "vid": "4",
        "type": "book",
        "language": "und",
        "title": "test",
        "uid": "1",
        "status": "1",
        "created": "1452450395",
        "changed": "1452450395",
        "comment": "0",
        "promote": "1",
        "sticky": "0",
        "tnid": "0",
        "translate": "0",
        "uri": "http://localhost/drupal-test/api/books/node/4"
    },
    {
        "nid": "3",
        "vid": "3",
        "type": "book",
        "language": "und",
        "title": "test",
        "uid": "1",
        "status": "1",
        "created": "1452450374",
        "changed": "1452450374",
        "comment": "0",
        "promote": "1",
        "sticky": "0",
        "tnid": "0",
        "translate": "0",
        "uri": "http://localhost/drupal-test/api/books/node/3"
    },
    {
        "nid": "2",
        "vid": "2",
        "type": "book",
        "language": "und",
        "title": "test",
        "uid": "1",
        "status": "1",
        "created": "1452450354",
        "changed": "1452450354",
        "comment": "0",
        "promote": "1",
        "sticky": "0",
        "tnid": "0",
        "translate": "0",
        "uri": "http://localhost/drupal-test/api/books/node/2"
    },
    {
        "nid": "1",
        "vid": "1",
        "type": "book",
        "language": "und",
        "title": "test",
        "uid": "1",
        "status": "1",
        "created": "1452450332",
        "changed": "1452450332",
        "comment": "0",
        "promote": "1",
        "sticky": "0",
        "tnid": "0",
        "translate": "0",
        "uri": "http://localhost/drupal-test/api/books/node/1"
    }
]
```

### 2. 获取单个node：

#### 请求：

```sh
GET /drupal-test/api/books/node/1 HTTP/1.1
Host: localhost
Cache-Control: no-cache
```

#### 返回：

```json
{
    "vid": "1",
    "uid": "1",
    "title": "test",
    "log": "",
    "status": "1",
    "comment": "0",
    "promote": "1",
    "sticky": "0",
    "nid": "1",
    "type": "book",
    "language": "und",
    "created": "1452450332",
    "changed": "1452453629",
    "tnid": "0",
    "translate": "0",
    "revision_timestamp": "1452453629",
    "revision_uid": "1",
    "body": {
        "und": [
            {
                "value": "this is a testing book node",
                "summary": "",
                "format": "plain_text",
                "safe_value": "<p>this is a testing book node</p>\n",
                "safe_summary": ""
            }
        ]
    },
    "name": "lyon",
    "picture": "0",
    "data": "b:0;",
    "path": "http://localhost/drupal-test/node/1"
}
```

当然，上述两个请求也是在未注册用户有view published content权限的情况下才能成功。如果未注册用户并没有该权限，那么返回的数据会是：

```json
[
  "Access denied for user anonymous"
]
```

同样地，在发起CREATE, PUT, DELETE请求时，也是需要有authentication的。这部分内容将留在下一篇文章里陈述。
