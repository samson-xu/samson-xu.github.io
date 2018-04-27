---
title: 淘宝npm镜像使用方法
date: 2018-04-26 17:54:18
tags:
- npm
categories:
- Web
- Hexo
comments:
---

淘宝 npm 地址： <http://npm.taobao.org/>

# 临时使用
```
npm --registry https://registry.npm.taobao.org install express
```

# 持久使用
```
npm config set registry https://registry.npm.taobao.org
# 配置后可通过下面方式来验证是否成功
npm config get registry
# 或
npm info express
```

# 通过cnpm使用
```
npm install -g cnpm --registry=https://registry.npm.taobao.org
# 使用
cnpm install express
```
