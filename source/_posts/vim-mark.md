---
title: vim书签管理
date: 2018-06-11 14:13:16
tags:
- vim
categories:
- Linux
comments:
---

# 简介
书签是vim中非常强大的一个功能，书签分为文件书签跟全局书签。
文件书签是你标记文件中的不同位置，然后可以在文件内快速跳转到你想要的位置。
全局书签是标记不同文件中的位置，也就是说你可以在不同的文件中快速跳转。

# 命令
```
m{a-zA-Z}       -> 保存书签
                    小写的是文件书签，可以用(a-z）中的任何字母标记。
                    大写的是全局书签，用大写的(A-Z)中任意字母标记。
`{a-zA-Z}       -> 跳转到某个书签。
                    如果是全局书签，则会开启被书签标记的文件跳转至标记的行
`0              -> 跳转入现在编辑的文件中上次退出的位置 (go to last exit in file)
``              -> 跳转如最后一次跳转的位置 (go to last jump -> go back to last jump)
```             -> 跳转至最后一次编辑的位置 (go to last edit)
g`{mark}        -> 跳转到书签 (jump to {mark})
:delm {marks}   -> 删除一个书签 (delete a mark)
                    例如:delm a那么就删除了书签a
:delm!          -> 删除全部书签 (delete all marks)
:marks          -> 显示系统全部书签 (show all bookmarks)
```
