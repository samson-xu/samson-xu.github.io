---
title: yum常用命令
date: 2017-07-13 16:17:22
tags:
- yum
categories:
- Linux
comments:
---

# 使用yum安装和卸载软件，有个前提是yum安装的软件包都是rpm格式的
安装的命令是，yum install ~，yum会查询数据库，有无这一软件包，如果有，则检查其依赖冲突关系，如果没有依赖冲突，那么最好，下载安装;如果有，则会给出提示，询问是否要同时安装依赖，或删除冲突的包，你可以自己作出判断；
删除的命令是，yum remove ~，同安装一样，yum也会查询数据库，给出解决依赖关系的提示。
其中~ 代表软件名

    1.用YUM安装软件包命令：yum install ~
    2.用YUM删除软件包命令：yum remove ~

# 用yum查询想安装的软件
我们常会碰到这样的情况，想安装一个软件，只知道它和某方面有关，但又不能确切知道它的名字。这时yum的查询功能就起作用了。我们可以用 yum search keyword这样的命令来进行搜索，比如我们要则安装一个Instant Messenger，但又不知到底有哪些，这时不妨用 yum search messenger这样的指令进行搜索，yum会搜索所有可用rpm的描述，列出所有描述中和messeger有关的rpm包，于是我们可能得到 gaim，kopete等等，并从中选择。
有时我们还会碰到安装了一个包，但又不知道其用途，我们可以用yum info packagename这个指令来获取信息。

      1.使用YUM查找软件包
      命令：yum search ~
      2.列出所有可安装的软件包
      命令：yum list
      3.列出所有可更新的软件包
      命令：yum list updates
      4.列出所有已安装的软件包
      命令：yum list installed
      5.列出所有已安装但不在Yum Repository 內的软件包
      命令：yum list extras
      6.列出所指定软件包
      命令：yum list ～
      7.使用YUM获取软件包信息
      命令：yum info ～
      8.列出所有软件包的信息
      命令：yum info
      9.列出所有可更新的软件包信息
      命令：yum info updates
      10.列出所有已安裝的软件包信息
      命令：yum info installed
      11.列出所有已安裝但不在Yum Repository 內的软件包信息
      命令：yum info extras
      12.列出软件包提供哪些文件
      命令：yum provides~
# 清除YUM缓存
yum 会把下载的软件包和header存储在cache中，而不会自动删除。如果我们觉得它们占用了磁盘空间，可以使用yum clean指令进行清除，更精确的用法是yum clean headers清除header，yum clean packages清除下载的rpm包，yum clean all 清除所有。

     1.清除缓存目录(/var/cache/yum)下的软件包
     命令：yum clean packages
     2.清除缓存目录(/var/cache/yum)下的 headers
     命令：yum clean headers
     3.清除缓存目录(/var/cache/yum)下旧的 headers
     命令：yum clean oldheaders
     4.清除缓存目录(/var/cache/yum)下的软件包及旧的headers
     命令：yum clean, yum clean all (= yum clean packages; yum clean oldheaders)
# yum命令工具使用举例
     yum update  升级系统
     yum install  ～ 安装指定软件包
     yum update ～ 升级指定软件包
     yum remove ～ 卸载指定软件
     yum grouplist   查看系统中已经安装的和可用的软件组，可用的可以安装
     yum grooupinstall ～安装上一个命令显示的可用的软件组中的一个
     yum grooupupdate ～更新指定软件组的软件包
     yum grooupremove ～ 卸载指定软件组中的软件包
     yum deplist ～ 查询指定软件包的依赖关系
     yum list yum\* 列出所有以yum开头的软件包
     yum localinstall ～ 从硬盘安装rpm包并使用yum解决依赖
