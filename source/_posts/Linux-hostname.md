---
title: Linux修改主机名
date: 2018-05-10 10:47:14
tags:
- hostname
categories:
- Linux
comments:
---
Linux系统安装好后，都会有默认的主机名，这里以CentOS系统为例，默认的主机名为localhost.localdomain，为了便于使用，我们常常需要修改主机名，下面演示的是永久更改主机名的方法。

# 登录
以根用户登录，或者登录后切换到根用户，然后在提示符下输入hostname命令，可以看出当前系统的主机名为localhost.localdomain。

# 修改network文件
更改/etc/sysconfig下的network文件，在提示符下输入vi /etc/sysconfig/network，然后将HOSTNAME后面的值改为想要设置的主机名。

# 修改hosts文件
更改/etc下的hosts文件，在提示符下输入vi /etc/hosts，然后将localhost.localdomain改为想要设置的主机名。

# 重启服务器
```
reboot
```

# 查看是否生效
```
hostname
```

# 解析
/etc/sysconfig/network   修改这个文件，系统才有效
/etc/hosts       hostname命令读这个配置文件
