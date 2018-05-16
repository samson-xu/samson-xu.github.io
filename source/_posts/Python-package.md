---
title: Linux下Python模块安装
date: 2018-05-16 16:43:40
tags:
categories:
- Python
comments:
---

# 查看Python安装路径
```
whereis python
```
或
```
python # 进入python cmd
import sys
sys.path
```

# 查看Python已安装模块
## pydoc命令
```
pydoc modules
```

## help命令
```
help("modules") # 在python交互式解释器中输入此命令
```

## 导入sys模块查看
```
import sys
sys.modules.keys()
```

## pip命令
> 如果你使用的是pip来作为你的python包管理器的话，可以在命令行下直接运行$ pip freeze或者$ pip list来查看安装包的信息，当然其它的包管理器也有类似的功能，同时，你也可以在python交互式解释器中导入pip模块来查看包信息
```
import pip
installed_packages = pip.get_installed_distributions()
installed_packages_list = sorted(["%s==%s" % (i.key, i.version)
     for i in installed_packages])
print(installed_packages_list)
```

## yolk命令
> 如果你安装过yolk的话可以使用yolk命令来查看包信息，你可以使用$ pip install yolk来安装它
yolk使用简单，只需在命令行下操作即可
```
$ yolk -l    #列出所有安装模块
$ yolk -a    #列出激活的模块
$ yolk -n    #列出非激活模块
$ yolk -U [packagename]  # 通过查询pypi来查看（该）模块是否有新版本
```

# Python模块安装
##  单文件模块
直接把文件拷贝到 $python_dir/Lib

## 多文件模块，带setup.py
下载模块包，进行解压，进入模块文件夹，执行：
```
python setup.py install
```

## easy_install方式
先下载ez_setup.py,运行python ez_setup 进行easy_install工具的安装，之后就可以使用easy_install进行安装package了。
```
easy_install  packageName
easy_install  package.egg
```

## pip 方式
先进行pip工具的安裝：easy_install pip（pip 可以通过easy_install 安裝，而且也会装到 Scripts 文件夹下。）
```
安裝：pip install PackageName
更新：pip install -U PackageName
移除：pip uninstall PackageName
搜索：pip search PackageName
帮助：pip help
```
