---
title: 普通用户使用Docker
date: 2017-07-06 16:23:21
tags:
- Docker
categories:
- Docker
comments:
---

1. 创建docker组
``` bash
$ sudo groupadd docker
```

2. 将当前用户加入docker组
``` bash
sudo gpasswd -a ${USER} docker
```

3. 重新启动docker服务（下面是CentOS7的命令）
``` bash
sudo systemctl restart docker
```

4. 当前用户退出系统重新登陆
``` bash
docker ps
```