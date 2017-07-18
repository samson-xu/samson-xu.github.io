---
title: CentOS下移动硬盘挂载
date: 2017-07-18 10:35:47
tags:
- 挂盘
categories:
- Linux
comments:
---

# 安装NTFS-3G
```
./configure
make
make install
```

# 查看接入设备路径
```
fdisk -l
```

# 移动硬盘挂载
```
mount -t ntfs-3g 设备路径 挂载路径
```

# 移动硬盘卸载
```
umount 挂载路径
```