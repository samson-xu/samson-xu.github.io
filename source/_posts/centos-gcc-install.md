---
title: 在CentOS下编译安装GCC
date: 2017-08-30 11:26:02
tags:
- GCC
categories:
- Linux
comments:
---

# 下载源码
```buildoutcfg
wget https://mirrors.tuna.tsinghua.edu.cn/gnu/gcc/gcc-4.8.0/gcc-4.8.0.tar.gz
```

# 下载依赖包
```buildoutcfg
tar zxvf gcc-4.8.0.tar.gz
cd gcc-4.8.0
./contrib/download_prerequisites
```

# 编译安装
```buildoutcfg
mkdir gcc-build-4.8.0
mkdir gcc-install-4.8.0
cd gcc-build-4.8.0
../configure --prefix=/path/to/gcc-install-4.8.0
make && make install
```

# 环境变量配置
在/etc/profile增加以下内容，对所有用户有效；在Home目录下的.bashrc或.bash_profile里增加下面的内容，只对当前用户有效。(注意：等号前面不要加空格,否则可能出现 command not found)
```buildoutcfg
#在PATH中找到可执行文件程序的路径。
export PATH=$PATH:$HOME/bin

#gcc找到头文件的路径
C_INCLUDE_PATH=/usr/include
export C_INCLUDE_PATH

#g++找到头文件的路径
CPLUS_INCLUDE_PATH=/usr/include
export CPLUS_INCLUDE_PATH

#找到动态链接库的路径
LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/MyLib 
export LD_LIBRARY_PATH

#找到静态库的路径
LIBRARY_PATH=$LIBRARY_PATH:/MyLib
export LIBRARY_PATH

```

# 查看版本号
```buildoutcfg
gcc --version
gcc (GCC) 4.8.5

g++ --version
g++ (GCC) 4.8.5

which gcc
/usr/bin/gcc

which g++
/usr/bin/g++
```

# 测试程序
创建一个 main.cpp 文件，内容如下：
```buildoutcfg
  #include <iostream>
    using namespace std;
    int main() {
        cout << "Hello world!" << endl;
        return 0;
    }
```

编译 main.cpp，执行如下命令：
```buildoutcfg
g++ main.cpp -o main
```

执行生成的文件
```buildoutcfg
./main
```

输出结果如下
```buildoutcfg
Hello world!
```
