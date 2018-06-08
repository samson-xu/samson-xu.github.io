---
title: Python 文件类型
date: 2018-06-08 17:20:29
tags:
categories:
- Python
comments:
---

# 简介
Python 并非完全是解释性语言，它也存在编译。先将源码文件 *.py 编译为 *.pyc/*.pyo，然后由 Python 的虚拟机执行。相对于 *.py 文件来说，编译为 *.pyc/*.pyo 本质上和 *.py 没有太大区别，只是提高了模块的加载速度，并没有提高代码的执行速度。

# 文件类型
* *.py：源码文件，由 Python 程序解释。
* *.pyc：源码经编译后生成的二进制字节码（Bytecode）文件。
* *.pyo：优化编译后的程序，也是二进制字节码文件。

# 生成 *.pyc 文件
假设，有一个名为 hello.py 的源文件：
```
print("Hello World!")
```
要编译为 *.pyc 文件，需要引入 Python 中的模块 py_compile，在交互模式下输入：
```
>>> import py_compile
>>> py_compile.compile("hello.py")
```
这样，*.pyc 文件就生成了：
```
$ ls
hello.py  hello.pyc
```
编译之后的是一个二进制文件
# 生成 *.pyo 文件
要编译为 *.pyo 文件，需要通过 Python 解释器的选项去编译：
```
python -O -m py_compile hello.py
```
这样，*.pyo 文件就生成了：
```
$ ls
hello.py  hello.pyc  hello.pyo
```
由于经过优化，所以，一般在大小上，*.pyo 文件小于等于 *.pyc 文件。

# 效率对比
*.pyc/*.pyo 和 *.py 文件一样，都可以被执行：
```
$ python hello.py
Hello World!
$ python hello.pyc
Hello World!
$ python hello.pyo
Hello World!
```
运行速度相差无几，加载速度 *.pyc/*.pyo 稍占优势。当然，除此之外，还有一个很大的优点：隐藏源码！
>注意： Python 3.5 中不再使用 *.pyo 文件，而是引入了一种更灵活的替代机制，*.pyc 文件可以表示优化和未优化的字节码。优化级别信息可以包含在 *.pyc 文件的名字中，具体可参见：PEP 488。
