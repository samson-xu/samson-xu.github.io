---
title: Linux swap分区配置
date: 2018-05-09 17:56:42
tags:
- swap
categories:
- Linux
comments:
---

我们一般所说的swap，指的是一个交换分区或文件。从功能上讲，交换分区主要是在内存不够用的时候，将部分内存上的数据交换到swap空间上，以便让系统不会因内存不够用而导致oom或者更致命的情况出现。所以，当内存使用存在压力，开始触发内存回收的行为时，就可能会使用swap空间。

# 生成swap文件
先填充一个8G的文件，用做交换分区：
```
dd if=/dev/zero of=/var/swap bs=1024 count=8388608
```

# 格式化swap文件
```
mkswap /var/swap
```

# 加载swap文件
加载这个交换文件：
```
swapon /var/swap
```
同时将其设置为每次开机就挂载，在/etc/fstab追加一行：

```
/var/swap swap swap defaults 0 0
```

# 测试是否加载成功
运行以下脚本测试是否使用到交换分区
```
#!/bin/bash
mkdir /tmp/memory
# 根据具体情况设置内存大小，此处设置为1024M
mount -t tmpfs -o size=1024M tmpfs /tmp/memory
dd if=/dev/zero of=/tmp/memory/block
sleep 3600
rm /tmp/memory/block
umount /tmp/memory
rmdir /tmp/memory
```

# 查看当前加载的交换分区信息
```
swapon -s
# 等价于
cat /proc/swaps
```

# 卸载swap分区
```
#使用swapoff来卸载已经挂载的交换文件，卸载的同时将/etc/fstab中对应的挂载项删除
swapoff /var/swap
```

