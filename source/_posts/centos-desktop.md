---
title: CentOS 6 minimal版系统安装图形化界面
date: 2018-06-11 14:08:58
tags:
categories:
- Linux
comments:
---

# 安装Desktop组
```
[root@local ~]# yum groupinstall "Desktop" -y
```

# 安装 X Window System
```
[root@local ~]# yum groupinstall "X Window System" -y
```

# 安装中文支持（可选）
```
[root@local ~]#  yum groupinstall "Chinese Support" -y
```

# 运行级别改为5
```
[root@local ~]# tail -1 /etc/inittab
id:5:initdefault:
```

# 重启系统
```
[root@local ~]# reboot
```
