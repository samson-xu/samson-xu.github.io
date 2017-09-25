---
title: 关于gcc、glibc和binutils模块之间的关系
date: 2017-09-25 10:31:13
tags:
- glibc
categories:
- Linux
comments:
---

# 关于gcc、glibc和binutils模块之间的关系
  1.  gcc（gnu collect compiler）是一组编译工具的总称。它主要完成的工作任务是“预处理”和“编译”，以及提供了与编译器紧密相关的运行库的支持，如libgcc_s.so、libstdc++.so等。
  2.  binutils提供了一系列用来创建、管理和维护二进制目标文件的工具程序，如汇编（as）、连接（ld）、静态库归档（ar）、反汇编（objdump）、elf结构分析工具（readelf）、无效调试信息和符号的工具（strip）等。通常，binutils与gcc是紧密相集成的，没有binutils的话，gcc是不能正常工作的。
  3.  glibc是gnu发布的libc库，也即c运行库。glibc是linux系统中最底层的api（应用程序开发接口），几乎其它任何的运行库都会倚赖于glibc。glibc除了封装linux操作系统所提供的系统服务外，它本身也提供了许多其它一些必要功能服务的实现，主要的如下：
 （1）string，字符串处理
 （2）signal，信号处理
 （3）dlfcn，管理共享库的动态加载
 （4）direct，文件目录操作
 （5）elf，共享库的动态加载器，也即interpreter
 （6）iconv，不同字符集的编码转换
 （7）inet，socket接口的实现
 （8）intl，国际化，也即gettext的实现
 （9）io
 （10）linuxthreads
 （11）locale，本地化
 （12）login，虚拟终端设备的管理，及系统的安全访问
 （13）malloc，动态内存的分配与管理
 （14）nis
 （15）stdlib，其它基本功能

# 在现有系统上如何升级（redhat9上实践的）

1. 升级这些库时，最好不要覆盖系统中缺省的；因为这些库，尤其是glibc库，是系统中最核心的共享库和工具，如果盲目覆盖，很可能导致整个系统瘫痪，因为一般更新glibc库时，其它所有以来libc库的共享库都需要重新被编译一遍。因此，为了调试某个程序进入glibc时，最好把glibc安装到/usr/local/lib下。

2. 首先编译glibc库。注意最好令建立一个glibc-build的目录，configure时加上--enable-add-ons=linuxthreads选项。make install安装到/usr/local下。

3. 修改gcc的spec文件（/usr/lib/gcc-lib/i386-redhat-linux/3.2.2/specs），更改ld-linux.so.2为/usr/local/lib下的新的共享库装载器。

4. 编译binutils库，此时被编译出的程序会连接到/usr/local/lib下的新的libc库。注意，在configure前，需要设置ld缺省连接的路径（LIBRARY_PATH=/usr/local/lib:/lib:/usr/lib），否则binutils会configure出错，找不到libc中的一些符号。具体步骤如下：
 （1）export LIBRARY_PATH=/usr/local/lib:/lib:/usr/lib
 （2）mkdir binutils-build && cd binutils-build
 （3）../binutils-2.13.90.0.18/configure
 （4）make
 （5）make -C ld clean
 （6）make -C ld LIB_PATH=/usr/lib:/lib:/usr/local/bin（设置编译后的ld的缺省库搜索路径，后面的比前面的优先级高）
 （7）make install


# 总结

1. 运行时，动态库的装载依赖于ld-linux.so.6的实现，它查找共享库的顺序如下：
 （1）ld-linux.so.6在可执行的目标文件中被指定，可用readelf命令查看
 （2）ld-linux.so.6缺省在/usr/lib和lib中搜索；当glibc安装到/usr/local下时，它查找/usr/local/lib
 （3）LD_LIBRARY_PATH环境变量中所设定的路径
 （4）/etc/ld.so.conf（或/usr/local/etc/ld.so.conf）中所指定的路径，由ldconfig生成二进制的ld.so.cache中


2. 编译时，搜索库的路径顺序如下：
 （1）ld-linux.so.6由gcc的spec文件中所设定
 （2）gcc --print-search-dirs所打印出的路径，主要是libgcc_s.so等库。可以通过GCC_EXEC_PREFIX来设定
 （3）LIBRARY_PATH环境变量中所设定的路径，或编译的命令行中指定的-L/usr/local/lib 
 （2）binutils中的ld所设定的缺省搜索路径顺序，编译binutils时指定。（可以通过“ld --verbose | grep SEARCH”来查看）


3. 二进制程序的搜索路径顺序为PATH环境变量中所设定。一般/usr/local/bin高于/usr/bin


4. 编译时的头文件的搜索路径顺序，与library的查找顺序类似。一般/usr/local/include高于/usr/include
