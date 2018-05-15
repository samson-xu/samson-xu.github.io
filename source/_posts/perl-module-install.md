---
title: Perl模块安装
date: 2018-05-15 16:52:01
tags:
- Perl
categories:
- Perl
comments:
---

# 查看已安装模块
perllocal 可以列出每个安装的模块的信息，如安装的时间、安装的位置、版本信息等
```
perldoc perllocal
```

或者

```
perldoc 模块名
```
如果已经安装该模块，上述命令会弹出该模块的帮助文档

# Perl模块安装
## 手动安装
去CPAN搜索下载需要的模块，参考README，运行如下命令：
```
perl makefile.pl
make
make install
```

## 自动安装
```
# perl -MCPAN -e shell  //进入cpan界面
cpan> install xxx       //xxx为要安装的perl模块，当然也可以直接# perl –MCPAN –e 'install xxx'
```

如果CentOS系统没有安装CPAN，需要运行如下命令安装：
```
sudo yum -y install perl-CPAN
```
