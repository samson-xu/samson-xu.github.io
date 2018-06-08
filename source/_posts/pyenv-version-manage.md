---
title: Python多版本共存管理工具-pyenv
date: 2018-06-08 17:08:40
tags:
- pyenv
categories:
- Python
comments:
---

# 问题
* 系统自带的Python是2.6，自己需要Python 2.7中的某些特性；
* 系统自带的Python是2.x，自己需要Python 3.x；
* 此时需要在系统中安装多个Python，但又不能影响系统自带的Python，即需要实现Python的多版本共存。pyenv就是这样一个Python版本管理器。

# 安装pyenv
```
$ git clone git://github.com/pyenv/pyenv.git ~/.pyenv
$ echo 'export PATH="$HOME/.pyenv/bin:$PATH"' >> ~/.bashrc
$ echo 'eval "$(pyenv init -)"' >> ~/.bashrc
$ exec $SHELL -l
```

# 安装Python
查看可安装的版本
```
$ pyenv install --list
```
该命令会列出可以用pyenv安装的Python版本，仅列举几个:
2.7.8 # Python 2版本
3.4.1 # Python 3版本
anaconda-2.0.1 # 支持Python 2.6和2.7
anaconda3-2.0.1 # 支持Python 3.3和3.4
其中形如x.x.x这样的只有版本号的为Python官方版本，其他的形如xxxxx-x.x.x这种既有名称又有版本后的属于“衍生版”或发行版。

## 安装Python的依赖包
在安装Python时需要首先安装其依赖的其他软件包，已知的一些需要预先安装的库如下。
在CentOS/RHEL/Fedora下:
```
sudo yum install readline readline-devel readline-static
sudo yum install openssl openssl-devel openssl-static
sudo yum install sqlite-devel
sudo yum install bzip2-devel bzip2-libs
```

## 安装指定版本
使用如下命令即可安装python 3.4.1：
```
$ pyenv install 3.4.1 -v
```
该命令会从github上下载python的源代码，并解压到/tmp目录下，然后在/tmp中执行编译工作。若依赖包没有安装，则会出现编译错误，需要在安装依赖包后重新执行该命令。
对于科研环境，更推荐安装专为科学计算准备的Anaconda发行版，pyenv install anaconda-2.1.0安装2.x版本，pyenv install anaconda3-2.1.0安装3.x版本；Anacoda很大，用pyenv下载会比较慢，可以自己到Anaconda官方网站下载，并将下载得到的文件放在~/.pyenv/cache目录下，则pyenv不会重复下载。

##  更新数据库
安装完成之后需要对数据库进行更新：
```
$ pyenv rehash
```
查看当前已安装的python版本
```
$ pyenv versions
* system (set by /home/seisman/.pyenv/version)
3.4.1
```
其中的星号表示当前正在使用的是系统自带的python。

##  设置全局的python版本
```
$ pyenv global 3.4.1
$ pyenv versions
system
* 3.4.1 (set by /home/seisman/.pyenv/version)
```
当前全局的python版本已经变成了3.4.1。也可以使用pyenv local或pyenv shell临时改变python版本。

## 确认python版本
```
$ python
Python 3.4.1 (default, Sep 10 2014, 17:10:18)
[GCC 4.4.7 20120313 (Red Hat 4.4.7-1)] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>>
```

# 使用python
* 输入python即可使用新版本的python。
* 系统自带的脚本会以/usr/bin/python的方式直接调用老版本的python，因而不会对系统脚本产生影响。
* 使用pip安装第三方模块时会安装到~/.pyenv/versions/3.4.1下，不会和系统模块发生冲突。
* 使用pip安装模块后，可能需要执行pyenv rehash更新数据库。
