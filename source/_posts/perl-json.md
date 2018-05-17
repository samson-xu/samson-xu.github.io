---
title: 在 Perl 中使用 JSON
date: 2018-05-17 09:43:06
tags:
- JSON
categories:
- Perl
comments:
---

# 环境
在开始使用 Perl 编码和解码 JSON 之前，我们需要安装 JSON 模块，可以从 CPAN 中获取。下载 JSON-2.53.tar.gz 或者其他任意最新版本之后请按照下列步骤操作：
```
$ tar -xvfz JSON-2.53.tar.gz
$ cd JSON-2.53
$ perl Makefile.PL
$ make
$ make install
```
# JSON 函数
|函数	|程序库|
| ---------- | :----------: |
|encode_json	|将给定的 Perl 数据结构转为 UTF-8 编码的二进制字符串。|
|decode_json	|解码 JSON 字符串。|
|to_json	|将给定的 Perl 数据结构转换为 JSON 字符串。|
|from_json	|接受一个 JSON 字符串并试图解析它，返回结果引用。|
|convert_blessed	|给这个函数传递 true，则 Perl 可以使用这个对象类的 TO_JSON 方法将对象转换为 JSON。|

# 使用 Perl 编码 JSON（encode_json）
Perl 的 encode_json() 函数可以将给定的 Perl 数据结构转换为 UTF-8 编码的二进制字符串。
## 语法
```
$json_text = encode_json ($perl_scalar );
or
$json_text = JSON->new->utf8->encode($perl_scalar);
```
## 示例
下面的例子展示了使用 Perl 将数组转换为 JSON:
```
#!/usr/bin/perl
use JSON;
my %rec_hash = ('a' => 1, 'b' => 2, 'c' => 3, 'd' => 4, 'e' => 5);
my $json = encode_json \%rec_hash;
print "$json\n";
```
执行时生成如下所示结果:
```
{"e":5,"c":3,"a":1,"b":2,"d":4}
```
下面的例子展示了如何将 Perl 对象转换为 JSON：
```
#!/usr/bin/perl
package Emp;
sub new
{
    my $class = shift;
    my $self = {
    name => shift,
        hobbies => shift,
        birthdate => shift,
    };
    bless $self, $class;
    return $self;
}
sub TO_JSON { return { %{ shift() } }; }

package main;
use JSON;
my $JSON = JSON->new->utf8;
$JSON->convert_blessed(1);

$e = new Emp( "sachin", "sports", "8/5/1974 12:20:03 pm");
$json = $JSON->encode($e);
print "$json\n";
```
执行时生成如下所示结果：
```
{"birthdate":"8/5/1974 12:20:03 pm","name":"sachin","hobbies":"sports"}
```

# 使用 Perl 解码 JSON（decode_json）
Perl 的 decode_json() 函数用于在 Perl 中解码 JSON。这个函数返回从 JSON 解码到适当 Perl 类型的值。
## 语法
```
$perl_scalar = decode_json $json_text
or
$perl_scalar = JSON->new->utf8->decode($json_text)
```
## 示例
下面的例子展示了如何使用 Perl 解码 JSON 对象。如果你的机器上没有 Data::Dumper 模块那么你需要安装这个模块。
```
#!/usr/bin/perl
use JSON;
use Data::Dumper;

$json = '{"a":1,"b":2,"c":3,"d":4,"e":5}';

$text = decode_json($json);
print Dumper($text);
```
执行时生成如下所示结果：
```
$VAR1 = {
    'e' => 5,
    'c' => 3,
    'a' => 1,
    'b' => 2,
    'd' => 4
};
```
