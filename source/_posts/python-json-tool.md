---
title: 解决python中json.tool中文乱码问题
date: 2018-05-17 09:34:17
tags:
- json.tool
categories:
- Python
comments:
---

Python中的json.tool模块用于对json文件进行格式化。
```
$ python -m json.tool in.json > out.json
```

然而有时候会有一个问题，就是若返回的 json 字符串中包含中文，那么这样打印出来之后，中文会变成以 \u 开头的转义形式，从而让程序员无法直接观察到中文的内容。这并非是一个 bug，而是 json 本身的标准，它要求 json 的内容都是 ascii 编码的。标准的 json 编码器和解码器都会遵循这一点。

解决这个问题的办法是编辑 json.tool 程序，该程序存在于 python 系统库安装路径下的 json/tool.py。在 main 方法的最后，将：
```
json.dump(obj, outfile, sort_keys=True, indent=4)
```
修改为（需提前 import codecs）
```
s = json.dumps(obj, sort_keys=True, indent=4, ensure_ascii=False)
outfile.write(codecs.encode(s, 'utf-8'))
```

打印的结果即可正常包含中文。
