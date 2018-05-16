---
title: 处理Linux终端中文乱码
date: 2018-05-16 17:34:59
tags:
- 乱码
categories:
- Linux
comments:
---

> 操作系统是无所谓中文版和英文版的，无论是windows还是Linux，系统发行的时候全世界都是一样的内核，系统呈现给我们是英文还是中文，完全取决于你选择的语言包。不同国家的人在安装使用的时候选择属于自己国家的语言包，应用程序中的语言也不是写死的，它根据系统的设置来调用相关的语言，所以，一个应用程序写出来不经过修改，全世界不同国家的用户都可以以母语界面使用它，这就事所谓的internationalization（国际化），简称 i18n。这也是未来软件的发展趋势。

# 查看系统当前默认字符集
```
# locale
```

# 安装中文包
```
# yum -y groupinstall chinese-support
```

# 修改系统文件
按如下内容，编辑/etc/sysconfig/i18n文件
```
LANG="zh_CN.UTF-8"
SYSFONT="latarcyrheb-sun16"
SUPPORTED="zh_CN.UTF-8:zh_CN:zh"
```

# 重启系统
```
reboot
```

# ssh远程终端设置
设置远程终端编码格式为UTF-8
