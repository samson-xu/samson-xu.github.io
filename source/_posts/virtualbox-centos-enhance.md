---
title: VirtualBox CentOS安装增强功能与设置共享文件夹
date: 2018-04-27 13:57:18
tags:
- CentOS
categories:
- Linux
comments:
---

# 设置CentOS 6.x 网络
默认情况下载的centos 6.x minimal是不开启网卡功能的，按照下面的步骤开启网卡。
 ```
 vi /etc/sysconfig/network-script/ifcfg-eth0
 # 将其中的
ONBOOT=no
修改为
ONBOOT=yes
#然后重新启动网络服务
service network restart
#此时应该就有网络了。使用下面的命令测试一下
ping -c 4 www.baidu.com
 ```

# 安装依赖环境
依次执行如下命令
```
yum install update
yum install kernel-headers
yum install kernel-devel
yum install gcc*
yum install make
```

重启系统
```
reboot
```

# 安装增强功能
点击VirtualBox工具栏的[设备]—[安装增强功能]，稍等片刻后，执行如下命令：
```
mkdir /mnt/cdrom
mount /dev/cdrom /mnt/cdrom
cd /mnt/cdrom
./VBoxLinuxAdditions.run
```

# 设置共享文件夹
首先在工具栏里的[设备]—[设置共享文件夹] 设置一个自己需要的文件夹，然后执行如下命令：
```
# 创建文件夹
mkdir /mnt/vboxshare
# 挂载共享文件夹
mount -t vboxsf host共享文件夹 /mnt/vboxshare/
# 下面是卸载操作
umount -f /mnt/vboxshare
# 设置开机自动挂载共享文件夹
在文件/etc/rc.d/rc.local添加如下命令
mount -t vboxsf host共享文件夹 /mnt/vboxshare/
```
