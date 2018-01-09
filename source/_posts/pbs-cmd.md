---
title: PBS作业管理系统简介
date: 2018-01-09 13:58:34
tags:
- PBS
categories:
- Linux
comments:
---

# 简介
PBS(Portable Batch System)最初由NASA的Ames研究中心开发，主要为了提供一个能满足异构计算网络需要的软件包，用于灵活的批处理，特别是满足高性能计算的需要，如集群系统、超级计算机和大规模并行系统。PBS的主要特点有：代码开放，免费获取；支持批处理、交互式作业和串行、多种并行作业，如MPI、PVM、HPF、MPL；PBS是功能最为齐全, 
历史最悠久, 支持最广泛的本地集群调度器之一。 PBS的目前包括openPBS, PBS Pro和Torque三个主要分支. 其中OpenPBS是最早的PBS系统, 目前已经没有太多后续开发,PBS pro是PBS的商业版本, 功能最为丰富. Torque是Clustering公司接过了OpenPBS, 并给与后续支持的一个开源版本.应用PBS提交任务则会形成任务队列，依次执行，有效分配资源，避免资源竞争。否则CPU时间片会轮流分配给各个人的任务，从而影响所有人的正常作业。

# qsub命令-作业提交
```buildoutcfg
qsub         [-a date_time][-A account_string][-c interval]
               [-C directive_prefix][-e path_name][-h][-j join_list][-k keep_list]
               [-m mail_options][-M mail_list][-N name]
               [-o path_name][-p priority][-q destination][-r y|n]
               [-S path_name_list][-u user_list][-v variable_list][-V]
               [-z][script]
```

# qstat命令-作业状态查询
## 命令格式
```buildoutcfg
qatat [-f][-a][-i] [-n][-s] [-R] [-Q][-q][-B][-u]
```

## 参数说明
-f jobid 列出指定作业的信息
-a 列出系统所有作业
-i 列出不在运行的作业
-n 列出分配给此作业的结点
-s 列出队列管理员与scheduler 所提供的建议
-R 列出磁盘预留信息
-Q 操作符是destination id，指明请求的是队列状态
-q 列出队列状态，并以alternative 形式显示
-au userid 列出指定用户的所有作业
-B 列出PBS Server 信息
-r 列出所有正在运行的作业
-Qf queue 列出指定队列的信息
-u 若操作符为作业号，则列出其状态。
若操作符为destination id，则列出运行在其上的属于user_list 中用户的作业状态。
例：# qstat -f 211 查询作业号为211 的作业的具体信息。

作业有如下几种状态：
C：作业完成
E：作业退出
H：作业挂起中
Q：作业排队中
R：作业运行中
T：作业被移走

# qdel命令-删除作业
```buildoutcfg
qdel [-W 间隔时间] 作业号
```

# 其它命令
pestat：整体查看节点状态
pbsnodes：详细查看节点状态

卸载并行存储命令：
/etc/init.d/LeoFS.20.1.1.98 stop

