---
title: Git中.gitignore的配置语法
date: 2017-07-25 09:43:50
tags:
- gitignore
categories:
- Git
comments:
---

# 语法规范

* 空行或是以#开头的行即注释行将被忽略。
* 可以在前面添加正斜杠/来避免递归,下面的例子中可以很明白的看出来与下一条的区别。
* 可以在后面添加正斜杠/来忽略文件夹，例如build/即忽略build文件夹。
* 可以使用!来否定忽略，即比如在前面用了*.apk，然后使用!a.apk，则这个a.apk不会被忽略。
* \*用来匹配零个或多个字符，如\*.[oa]忽略所有以".o"或".a"结尾，\*~忽略所有以~结尾的文件（这种文件通常被许多编辑器标记为临时文件）；[]用来匹配括号内的任一字符，如[abc]，也可以在括号内加连接符，如[0-9]匹配0至9的数；?用来匹配单个字符。



# 实例
```buildoutcfg
# 忽略以.a结尾的文件
*.a
# 但否定忽略lib.a,尽管已经在前面忽略了以.a结尾的文件
!lib.a
# 仅在当前目录下忽略TODO文件，但不包括子目录下的subdir/TODO
/TODO
# 忽略build/文件夹下的所有文件
build/
# 忽略doc/notes.txt,但不包括doc/server/arch.txt
doc/*.txt
# 忽略所有在doc/directory下，以.pdf为后缀的文件
doc/**/*.pdf
```

# 注意
Github只允许上传最大100MB的文件，如果超过，则会被server reject，需要如下配置：
```buildoutcfg
git filter-branch --force --index-filter "git rm --cached --ignore-unmatch Project1/Project1.1\ Sample\ Project/output.txt"  --prune-empty --tag-name-filter cat -- --all
git commit --amend -CHEAD
git push origin master
```