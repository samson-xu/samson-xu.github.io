---
title: Linux系统下文件插入列
date: 2018-05-15 17:28:18
tags:
- 插入列
categories:
- Linux
comments:
---

# sed
sed针对以字符为单位的列进行插入，例子如下：
```
# vim file
134 512 123
231 233 34
123 123 567

在第四列插入a：
# sed 's/./&a/4' file
134 a512 123
231 a233 34
123 a123 567
```

# awk
awk的操作不是针对一列列的字符，是针对一列列的字段。直接将要插入的列改变下就好了，比如在第2列后插入your words：
```
# vim file
134 512 123
231 233 34
123 123 567

# awk '$2=$2" your words"' file
134 512 your words 123
231 233 your words 34
123 123 your words 567
```
