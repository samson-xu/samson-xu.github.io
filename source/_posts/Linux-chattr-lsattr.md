---
title: Linux的chattr与lsattr命令详解
date: 2018-05-25 14:43:01
tags:
- chattr
- lsattr
categories:
- Linux
comments:
---

> 有时候你发现用root权限都不能修改某个文件，大部分原因是曾经用chattr命令锁定该文件了。chattr命令的作用很大，其中一些功能是由Linux内核版本来支持的。通过chattr命令修改属性能够提高系统的安全性，但是它并不适合所有的目录。chattr命令不能保护/、/dev、/tmp、/var目录。lsattr命令是显示chattr命令设置的文件属性。

# 命令功能
这两个命令是用来查看和改变文件、目录属性的，与chmod这个命令相比，chmod只是改变文件的读写、执行权限，更底层的属性控制是由chattr来改变的。

# chattr命令格式
```
chattr [ -RVf ] [ -v version ] [ mode ] files…
```
最关键的是在[mode]部分，[mode]部分是由+-=和[ASacDdIijsTtu]这些字符组合的，这部分是用来控制文件的属性。

# chattr命令参数
```
+ ：在原有参数设定基础上，追加参数。
- ：在原有参数设定基础上，移除参数。
= ：更新为指定参数设定。
A：文件或目录的 atime (access time)不可被修改(modified), 可以有效预防例如手提电脑磁盘I/O错误的发生。
S：硬盘I/O同步选项，功能类似sync。
a：即append，设定该参数后，只能向文件中添加数据，而不能删除，多用于服务器日志文件安全，只有root才能设定这个属性。
c：即compresse，设定文件是否经压缩后再存储。读取时需要经过自动解压操作。
d：即no dump，设定文件不能成为dump程序的备份目标。
i：设定文件不能被删除、改名、设定链接关系，同时不能写入或新增内容。i参数对于文件 系统的安全设置有很大帮助。
j：即journal，设定此参数使得当通过mount参数：data=ordered 或者 data=writeback 挂 载的文件系统，文件在写入时会先被记录(在journal中)。如果filesystem被设定参数为 data=journal，则该参数自动失效。
s：保密性地删除文件或目录，即硬盘空间被全部收回。
u：与s相反，当设定为u时，数据内容其实还存在磁盘中，可以用于undeletion。
```
各参数选项中常用到的是a和i。a选项强制只可添加不可删除，多用于日志系统的安全设定。而i是更为严格的安全设定，只有superuser (root) 或具有CAP_LINUX_IMMUTABLE处理能力（标识）的进程能够施加该选项。

# lsattr命令格式
```
lsattr [-RVadlv] [files...]
```
# lsattr命令参数
```
-R 　递归处理，将指定目录下的所有文件及子目录一并处理。
-V 　显示版本信息。
-a 　显示所有文件和目录，包括以"."为名称开头字符的额外内建，现行目录"."与上层目录".."。
-d 　显示，目录名称，而非其内容。
-l 　此参数目前没有任何作用。
-v 　显示文件或目录版本。
```


# 使用实例
1.用chattr命令防止系统中某个关键文件被修改：
```
# chattr +i /etc/resolv.conf
```

然后用mv /etc/resolv.conf等命令操作于该文件，都是得到Operation not permitted 的结果。vim编辑该文件时会提示W10: Warning: Changing a readonly file错误。要想修改此文件就要把i属性去掉:
```
# chattr -i /etc/resolv.conf
```

重新查看文件属性：
```
# lsattr /etc/resolv.conf
```
会显示如下属性：
```
----i-------- /etc/resolv.conf
```

2.让某个文件只能往里面追加数据，但不能删除，适用于各种日志文件：
```
# chattr +a /var/log/messages
```

# 使用限制
属性’c’, ‘s’和’u’可能在内核中并没有实现。’j’只适用于ext3文件系统。chattr属于e2fsprogs包的一部分，因此可认为你系统中的chattr命令和文件系统肯定是配套的。也意味着chattr/lsattr主要用于ext2/ext3/ext4文件系统中的文件或目录（可通过mount命令查看你要更改属性的文件是否位于ext文件系统中）。 实际上，只要文件系统在内核中实现了相应操作的ioctl（request为FS_IOC32_SETFLAGS/FS_IOC_SETFLAGS）的处理，就可以支持chattr。例如jfs、ubifs、reiserfs等文件系统目前也支持了chattr命令处理。对于不支持该命令的文件系统（如tmpfs、vfat、fuseblock等），在执行chattr时会报错。
