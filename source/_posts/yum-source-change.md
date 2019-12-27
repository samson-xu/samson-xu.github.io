---
title: Centos更换国内yum源
date: 2019-12-27 13:44:13
tags:
- yum
categories:
- Linux
comments:
---

## 下载wget工具
```buildoutcfg
yum install –y wget
```
## 进入yum源配置文件所在文件夹
```buildoutcfg
cd /etc/yum.repos.d/
```
## 备份本地yum源
```buildoutcfg
mv CentOS-Base.repo CentOS-Base.repo.bak
```
## 获取国内yum源（阿里、163二选一）
阿里云：
```buildoutcfg
wget -O CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo
```
163:
```buildoutcfg
wget -O CentOS-Base.repo http://mirrors.163.com/.help/CentOS7-Base-163.repo
```
## 清理缓存、重建缓存、升级Linux系统
清理yum缓存：
```buildoutcfg
yum clean all
```
重建缓存：
```buildoutcfg
yum makecache
```
升级Linux系统：
```buildoutcfg
yum -y update 
```