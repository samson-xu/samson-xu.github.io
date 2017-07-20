---
title: Linux终端通讯
date: 2017-07-20 09:11:58
tags:
- 通讯
categories:
- Linux
comments:
---

# wall命令
wall是给所有的用户发送消息，消息内容用''包含。
```
wall "Hello everybody, Please save your files and logout console, I will shutdown linux server in the ten minutes."
```

# write命令
先用who命令查看在线的用户以及他们的tty，然后用write命令给他发消息，输入该命令后就进入了消息模式，此时输入消息内容，回车就可以发送。退出按ctrl+D即可。

```
$ w

$ write userName tty
```

# mesg命令
如果不希望接受其他用户write的消息，用mesg -n关闭，再次开启为mesg -y

```
$ mesg -n

$ mesg -y
```