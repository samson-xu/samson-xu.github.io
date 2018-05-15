---
title: Perl时间处理模块-strftime
date: 2018-05-15 17:32:49
tags:
- strftime
categories:
- Perl
comments:
---

# localtime模块
以前我想大家都是使用的 localtime 来取得当地日期时间和日期。这个函数如果在标量环境时，会以字符串的形式来传回目前的时间和日期 。默认的 localtime 的函数是以 1970 到今天的秒来做整数计算的。默认这个程序会调用 time 的函数来给它提供一个值。
使用方法：
```
($sec, $min, $hour, $mday, $mon, $year, $wday, $yday, $isdst)=localtime;
$sec:秒
$min:分
$hour:小时
$mday:日
$mon:月
$year:目前的年减去1990，不是仅将19xx年的19去掉，因此不会有Y2K的困扰。
$wday:每周的日期(如Sunday是0)
$yday:每年的日期(如Jan 1是0)
$isdst:如果日光节约时间使用则是正值，其它为0。
```
上面这个函数常用，但是返回值非常乱，可读性非常不好，让我们很容易出错，所以我推荐 strftime 这个时间函数。当然，还有另一个模块 DataTime 也相当不错。不过 strftime 非常象 Linux 常用的 date 的命令。strftime 是 C 中 POSIX 的一个功能函数。被包含进了 Perl 中。

# strftime模块
示例：
```
#!/bin/env perl
use strict;
use warnings;
use POSIX qw(strftime);
print strftime("%Y-%m-%d %H:%M:%S/n", localtime(time));
```
Strftime 时间域:
```
% H 小时（00..23）
% I 小时（01..12）
% k 小时（0..23）
% l 小时（1..12）
% M 分（00..59）
% p 显示出AM或PM
% r 时间（hh：mm：ss AM或PM），12小时
% s 从1970年1月1日00：00：00到目前经历的秒数
% S 秒（00..59）
% T 时间（24小时制）（hh:mm:ss）
% X 显示时间的格式（％H:％M:％S）
% Z 时区 日期域
% a 星期几的简称（ Sun..Sat）
% A 星期几的全称（ Sunday..Saturday）
% b 月的简称（Jan..Dec）
% B 月的全称（January..December）
% c 日期和时间（ Mon Nov 8 14：12：46 CST 1999）
% d 一个月的第几天（01..31）
% D 日期（mm／dd／yy）
% h 和%b选项相同
% j 一年的第几天（001..366）
% m 月（01..12）
% w 一个星期的第几天（0代表星期天）
% W 一年的第几个星期（00..53，星期一为第一天）
% x 显示日期的格式（mm/dd/yy）
% y 年的最后两个数字（ 1999则是99）
% Y 年（例如：1970，1996等）
```

常用实例：
```
得到日期的全部

perl -MPOSIX -le 'print strftime "%c", localtime();'


得到普通的指定的日期

perl -MPOSIX -le 'print strftime "%a %d %b %Y %H:%M:%S %Z", localtime();'


得到一个小时以前的时间

perl -MPOSIX -le 'print strftime "%c", localtime(time()-3600);'

得到一天前的时间

perl -MPOSIX -le 'print strftime "%c", localtime(time()-86400);'

```

