---
title: SELinux管理
date: 2018-06-08 16:59:13
tags:
- SELinux
categories:
- Linux
comments:
---

# 查看SELinux状态
## getenforce
* getenforce 命令是单词get（获取）和enforce(执行)连写，可查看selinux状态，与setenforce命令相反
* setenforce 命令则是单词set（设置）和enforce(执行)连写，用于设置selinux防火墙状态，如： setenforce 0用于关闭selinux防火墙，但重启后失效
```
[root@localhost ~]# getenforce
Enforcing
```

## /usr/sbin/sestatus
Current mode表示当前selinux防火墙的安全策略
```
[root@localhost ~]# /usr/sbin/sestatus
SELinux status:                 enabled
SELinuxfs mount:                /sys/fs/selinux
SELinux root directory:         /etc/selinux
Loaded policy name:             targeted
Current mode:                   enforcing
Mode from config file:          enforcing
Policy MLS status:              enabled
Policy deny_unknown status:     allowed
Max kernel policy version:      28
```
SELinux status：selinux防火墙的状态，enabled表示启用selinux防火墙
Current mode： selinux防火墙当前的安全策略，enforcing 表示强

# 关闭SELinux
## 临时关闭
setenforce 0 ：用于关闭selinux防火墙，但重启后失效
```
[root@localhost ~]# setenforce 0
[root@localhost ~]# /usr/sbin/sestatus
SELinux status:                 enabled
SELinuxfs mount:                /sys/fs/selinux
SELinux root directory:         /etc/selinux
Loaded policy name:             targeted
Current mode:                   permissive
Mode from config file:          enforcing
Policy MLS status:              enabled
Policy deny_unknown status:     allowed
Max kernel policy version:      28
```

## 永久关闭
修改selinux的配置文件，重启后生效
打开 selinux 配置文件
```
[root@localhost ~]# vim /etc/selinux/config
```
修改 selinux 配置文件，将SELINUX=enforcing改为SELINUX=disabled，保存后退出
```
# This file controls the state of SELinux on the system.
# SELINUX= can take one of these three values:
#     enforcing - SELinux security policy is enforced.
#     permissive - SELinux prints warnings instead of enforcing.
#     disabled - No SELinux policy is loaded.
SELINUX=enforcing
# SELINUXTYPE= can take one of three two values:
#     targeted - Targeted processes are protected,
#     minimum - Modification of targeted policy. Only selected processes are protected.
#     mls - Multi Level Security protection.
SELINUXTYPE=targeted
```
此时获取当前selinux防火墙的安全策略仍为Enforcing，配置文件并未生效
```
[root@localhost ~]# getenforce
Enforcing
```
重启
```
[root@localhost ~]# reboot
```
验证
```
[root@localhost ~]# /usr/sbin/sestatus
SELinux status:                 disabled

[root@localhost ~]# getenforce
Disabled
```
