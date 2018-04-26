---
title: Linux系统配置查看-命令汇总
date: 2018-04-26 17:08:16
tags:
categories:
- Linux
comments:
---


# 查看Linux操作系统版本
```
[samson@work ~]$ head -n 1 /etc/issue
CentOS release 6.9 (Final)
```

# 查看计算机名
```
[samson@work ~]$ hostname
work
```

# 查看内核/操作系统/CPU信息的命令
```
[samson@work ~]$ uname -a
Linux work 2.6.32-696.23.1.el6.x86_64 #1 SMP Tue Mar 13 22:44:18 UTC 2018 x86_64 x86_64 x86_64 GNU/Linux
```

# 查看内存信息
```
[samson@work ~]$ cat /proc/meminfo
MemTotal:        2054216 kB
MemFree:         1865084 kB
Buffers:            7476 kB
Cached:            75372 kB
SwapCached:            0 kB
Active:            48128 kB
Inactive:          48020 kB
Active(anon):      13316 kB
Inactive(anon):      192 kB
Active(file):      34812 kB
Inactive(file):    47828 kB
Unevictable:           0 kB
Mlocked:               0 kB
SwapTotal:       4128764 kB
SwapFree:        4128764 kB
Dirty:                 4 kB
Writeback:             0 kB
AnonPages:         13320 kB
Mapped:             6880 kB
Shmem:               208 kB
Slab:              63876 kB
SReclaimable:       9772 kB
SUnreclaim:        54104 kB
KernelStack:        1488 kB
PageTables:         2048 kB
NFS_Unstable:          0 kB
Bounce:                0 kB
WritebackTmp:          0 kB
CommitLimit:     5155872 kB
Committed_AS:      89748 kB
VmallocTotal:   34359738367 kB
VmallocUsed:       32600 kB
VmallocChunk:   34359687672 kB
HardwareCorrupted:     0 kB
AnonHugePages:         0 kB
HugePages_Total:       0
HugePages_Free:        0
HugePages_Rsvd:        0
HugePages_Surp:        0
Hugepagesize:       2048 kB
DirectMap4k:       10176 kB
DirectMap2M:     2086912 kB
```

# 查看内存大小:
```
[samson@work ~]$ cat /proc/meminfo |grep MemTotal
MemTotal:        2054216 kB
```

# 查看存储大小:
```
[samson@work ~]$ df -h
Filesystem            Size  Used Avail Use% Mounted on
/dev/mapper/vg_work-lv_root
                       50G  1.3G   46G   3% /
tmpfs                 939M     0  939M   0% /dev/shm
/dev/sda1             477M   52M  400M  12% /boot
/dev/mapper/vg_work-lv_home
                       45G  107M   43G   1% /home
vboxshare             311G  5.5G  305G   2% /media/sf_vboxshare
vboxshare             311G  5.5G  305G   2% /mnt/vboxshare
```

# 查看CPU信息（型号）
```
[samson@work ~]$ cat /proc/cpuinfo | grep name | cut -f 2 -d : | uniq -c
      1  Intel(R) Core(TM) i5-6400 CPU @ 2.70GHz
```

# 查看CPU的主频
```
[samson@work ~]$ cat /proc/cpuinfo |grep MHz|uniq
cpu MHz		: 2712.002
```

# Linux总核数计算
```
总核数 = 物理CPU个数 X 每颗物理CPU的核数
总逻辑CPU数 = 物理CPU个数 X 每颗物理CPU的核数 X 超线程数
```

# 查看物理CPU个数
```
[samson@work ~]$ cat /proc/cpuinfo| grep "physical id"| sort -u | wc -l
1
```

# 查看每个物理CPU中core的个数(即核数)
```
[samson@work ~]$ cat /proc/cpuinfo| grep "cpu cores"| uniq
cpu cores	: 1
```

# 查看逻辑CPU的个数
```
[samson@work ~]$ cat /proc/cpuinfo| grep "processor"| wc -l
1
```





