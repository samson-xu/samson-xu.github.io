---
title: Git学习笔记
date: 2017-07-05 16:20:45
tags:
- Git
categories:
- Git
comments: true
---

1. 设置个人环境变量
``` bash
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
$ git config --global color.ui true
```

2. 初始化Git仓库
``` bash
$ git init
Initialized empty Git repository in /Users/michael/learngit/.git/
```

3. 添加文件到Git仓库
``` bash
$ git add file1.txt
$ git add file2.txt file3.txt
$ git commit -m "add 3 files."
```

4. git status查看工作区状态，git diff查看修改内容

5. HEAD指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令git reset --hard commit_id。

6. 穿梭前，用git log可以查看提交历史，以便确定要回退到哪个版本。

7. 要重返未来，用git reflog查看命令历史，以便确定要回到未来的哪个版本。

8. 当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令git checkout -- file。

9. 当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令git reset HEAD file，就回到了场景1，第二步按场景1操作。

10. 已经提交了不合适的修改到版本库时，想要撤销本次提交，参考版本回退一节，不过前提是没有推送到远程库。

11. 命令git rm用于删除一个文件。如果一个文件已经被提交到版本库，那么你永远不用担心误删，但是要小心，你只能恢复文件到最新版本，你会丢失最近一次提交后你修改的内容。

12. 添加远程仓库
``` bash
$ git remote add origin git@github.com:samson-xu/learngit.git
$ git push -u origin master
```
  由于远程库是空的，我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。此后，每次本地提交后，只要有必要，就可以使用命令git push origin master推送最新修改

13. 克隆远程库
``` bash
$ git clone git@github.com:michaelliao/gitskills.git
```
14. 分支管理命令
查看分支：git branch
创建分支：git branch <name>
切换分支：git checkout <name>
创建+切换分支：git checkout -b <name>
合并某分支到当前分支：git merge <name>
删除分支：git branch -d <name>
查看分支合并情况：git log --graph --pretty=oneline --abbrev-commit
强行删除一个没有被合并的分支： git branch -D <name>
推送不同的分支：git push origin dev

15. master分支用于发布稳定版本，平时在dev分支上开发， 合并分支时，加上--no-ff参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而fast forward合并就看不出来曾经做过合并。
``` bash
$ git merge --no-ff -m "merge with no-ff" dev
```

16. 工作区快照命令
存储当前工作区快照：git stash
查看工作区快照：git stash list
恢复工作区快照，但不删除stash内容： git stash apply stash@{0}
删除stash内容： git stash drop
恢复工作区快照，同时删除stash内容： git stash pop

17. 多人协作
查看远程库信息：git remote -v
从本地推送分支，使用git push origin branch-name，如果推送失败，先用git pull抓取远程的新提交
在本地创建和远程分支对应的分支，使用git checkout -b branch-name origin/branch-name，本地和远程分支的名称最好一致
建立本地分支和远程分支的关联，使用git branch --set-upstream branch-name origin/branch-name
从远程抓取分支，使用git pull，如果有冲突，要先处理冲突

18. 标签管理命令
命令git tag <name>用于新建一个标签，默认为HEAD，也可以指定一个commit id
git tag -a <tagname> -m "blablabla..."可以指定标签信息
git tag -s <tagname> -m "blablabla..."可以用PGP签名标签
命令git tag可以查看所有标签
git show <tagname>查看标签信息
命令git push origin <tagname>可以推送一个本地标签
命令git push origin --tags可以推送全部未推送过的本地标签
命令git tag -d <tagname>可以删除一个本地标签
命令git push origin :refs/tags/<tagname>可以删除一个远程标签

19. 忽略特殊文件
忽略某些文件时，需要编写.gitignore
.gitignore在线模板： https://github.com/github/gitignore
检查.gitignore规则命令：
``` bash
$ git check-ignore -v App.class
```

20. 配置别名
``` bash
$ git config --global alias.st status
```

21. 同步远程库
``` bash
$ git pull --rebase origin master
```