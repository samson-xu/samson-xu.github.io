---
title: Linux下R语言包安装
date: 2018-05-16 17:11:05
tags:
categories:
- R
comments:
---

# 查看R解释器版本
```
> sessionInfo()
```

# 查看包安装路径
```
> .libPaths()
```

# 查看已安装包
```
> installed.packages() # 列举详细信息
> .packages(all.available=T) # 列举包名
> library("XML") # 查看单个安装包
> help(package="XML") # 查看单个安装包
> search() # 查看当前载入的包
```

# R包安装
## 从CRAN安装
```
> install.packages('packageName')
```

## 从Github安装
```
#load devtools at first
> library(devtools)
> install_github('hadley/dplyr') #install from github, e.g. dplyr
```
> 实用devtools包中的函数install_github()来安装，需要指定仓库名（例子中的'hadley/'），这点通常比较难，因为很多包我们记不住这个。为此有人开发了另一个包，githubinstall，也是专门用来从github安装R包的，且用法类似于install.packages()，只需提供包的名字即可，如下代码示例：
```
#load githubinstall at first
> library(githubinstall)
> install_github('dplyr') #install from github, e.g. dplyr
```

## 从Bioconductor安装
```
#load bioconductor repository at first
> source("https://bioconductor.org/biocLite.R")
> biocLite('packageName') #install packageName from Bioconductor
```

# R包更新
```
update.packages( )
```

# R包卸除
```
>detach("package:packageName")
```
> 注意是卸除，不是卸载，也就是说不是把包从R运行环境中彻底删除，只是不希望该包被加载使用。
> 在包使用函数冲突，检验函数依赖时比较有用。

# R包卸载
```
remove.packages("packageName")
```
