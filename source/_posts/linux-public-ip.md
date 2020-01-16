---
title: 查看Linux主机公网IP
date: 2020-01-16 17:19:45
tags:
- IP
categories:
- Linux
comments:
---

## 查看Linux主机公网IP

 ```buildoutcfg
$ curl cip.cc
IP	: 119.39.48.120
地址	: 中国  湖南  长沙
运营商	: 联通

数据二	: 湖南省长沙市 | 联通

数据三	: 中国湖南长沙 | 联通

URL	: http://www.cip.cc/119.39.48.120
```
```buildoutcfg
$ curl ipinfo.io
{
  "ip": "119.39.48.120",
  "city": "Changsha",
  "region": "Hunan",
  "country": "CN",
  "loc": "28.1987,112.9709",
  "org": "AS4837 CHINA UNICOM China169 Backbone",
  "timezone": "Asia/Shanghai",
  "readme": "https://ipinfo.io/missingauth"
}
```

```buildoutcfg
$ curl myip.ipip.net
当前 IP：119.39.48.120  来自于：中国 湖南 长沙  联通
```