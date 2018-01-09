---
title: http协议简介
date: 2018-01-09 14:22:35
tags:
- http
categories:
- 网络
comments:
---

# URL详解
URL(Uniform Resource Locator) 地址用于描述一个网络上的资源,  基本格式如下
```buildoutcfg
schema://host[:port#]/path/.../[?query-string][#anchor]
scheme               指定低层使用的协议(例如：http, https, ftp)
host                 HTTP服务器的IP地址或者域名
port#                HTTP服务器的默认端口是80，这种情况下端口号可以省略。如果使用了别的端口，必须指明，例如 http://www.xyxu.online:8080/
path                 访问资源的路径
query-string         发送给http服务器的数据
anchor               锚
```

URL 的一个例子
```buildoutcfg
http://www.mywebsite.com/sj/test/test.aspx?name=sviergn&x=true#stuff

Schema: http
host: www.mywebsite.com
path: /sj/test/test.aspx
Query String: name=sviergn&x=true
Anchor: stuff
```
# HTTP协议是无状态的
http协议是无状态的，同一个客户端的这次请求和上次请求是没有对应关系，对http服务器来说，它并不知道这两个请求来自同一个客户端。 为了解决这个问题， Web程序引入了Cookie机制来维护状态.

# 打开一个网页需要浏览器发送很多次Request
1. 当你在浏览器输入URL http://www.xyxu.online 的时候，浏览器发送一个Request去获取 http://www.xyxu.online 的html.  服务器把Response发送回给浏览器.
2. 浏览器分析Response中的 HTML，发现其中引用了很多其他文件，比如图片，CSS文件，JS文件。
3. 浏览器会自动再次发送Request去获取图片，CSS文件，或者JS文件。
4. 等所有的文件都下载成功后。 网页就被显示出来了。
