---
title: 兼容Hexo的Markdown语法  
date: 2017-07-14 10:48:29  
tags:  
- Hexo  
- Markdown  
categories:  
- Web
- Hexo  
comments:  
---

# <center>Markdown 简介
&emsp;&emsp;Markdown 是一种用来写作的轻量级「标记语言」，它用简洁的语法代替排版，而不像一般我们用的字处理软件 Word 或 Pages 有大量的排版、字体设置。它使我们专心于码字，用「标记」语法，来代替常见的排版格式。


---  
# <center>基础语法
## 代码
```
*斜体*或_斜体_  
**粗体**  
***加粗斜体***  
~~删除线~~  
半方大的空白：&ensp;或&#8194;
全方大的空白：&emsp;或&#8195;
不断行的空白格：&nbsp;或&#160;
<center>居中
```
## 显示效果
*斜体*  或  _斜体_  
**粗体**  
***加粗斜体***  
~~删除线~~  
&ensp;半方大的空白  
&emsp;全方大的空白  
&nbsp;不断行的空白格
<center>居中


---
<center>**分级标题**
## 代码
```
# 一级标题
## 二级标题
### 三级标题
#### 四级标题
##### 五级标题
###### 六级标题
```
## 显示效果
# 一级标题
## 二级标题
### 三级标题
#### 四级标题
##### 五级标题
###### 六级标题


---
# <center>链接与图片
## 代码
```
欢迎来到我的博客[MyBlog](http://www.xyxu.online)
我的靓照![Me](http://osp5fgfht.bkt.clouddn.com/me.png-yy)
```
## 显示效果
欢迎来到我的博客[MyBlog](http://www.xyxu.online)
我的靓照![Me](http://osp5fgfht.bkt.clouddn.com/me.png-yy)
---
# <center>引用链接
## 代码
```
我经常去的几个网站[Baidu][1]、[Google][2]以及[我的博客][3]
[1]:http://www.baidu.com "Baidu"
[2]:http://www.Google.com "Google"
[3]:http://www.xyxu.online "我的博客"
```
## 显示效果
我经常去的几个网站[Baidu][1]、[Google][2]以及[我的博客][3]
[1]:http://www.baidu.com "Baidu"
[2]:http://www.Google.com "Google"
[3]:http://www.xyxu.online "我的博客"


---
# <center>自动链接
## 代码
```
<http://www.xyxu.online/>
<xy_xu@foxmail.com>
```
## 显示效果
<http://www.xyxu.online/>
<xy_xu@foxmail.com>


---
# <center>字体、字号与颜色
## 代码
```
<font face="黑体">我是黑体字</font>
<font face="微软雅黑">我是微软雅黑</font>
<font face="STCAIYUN">我是华文彩云</font>
<font color=#0099ff size=7 face="黑体">color=#0099ff size=72 face="黑体"</font>
<font color=#00ffff size=72>color=#00ffff</font>
<font color=gray size=72>color=gray</font>
```
## 显示效果
<font face="黑体">我是黑体字</font>
<font face="微软雅黑">我是微软雅黑</font>
<font face="STCAIYUN">我是华文彩云</font>
<font color=#0099ff size=7 face="黑体">color=#0099ff size=72 face="黑体"</font>
<font color=#00ffff size=72>color=#00ffff</font>
<font color=gray size=72>color=gray</font>


---
# <center>分割线与背景色
## 代码
```
分割线：三个以上的星号、减号、底线来建立一个分隔线
---  
***  
___  

背景色：
<table><tr><td bgcolor=orange>背景色是：orange</td></tr></table>
```
## 显示效果
---  
***  
___  
<table><tr><td bgcolor=orange>背景色是：orange</td></tr></table>


---
# <center>列表  
## 代码
```
使用 *，+，- 表示无序列表：
- 无序列表项 一
- 无序列表项 二
- 无序列表项 三

有序列表则使用数字接着一个英文句点：
1. 有序列表项 一
2. 有序列表项 二
3. 有序列表项 三
```
## 显示效果
- 无序列表项 一
- 无序列表项 二
- 无序列表项 三

1. 有序列表项 一
2. 有序列表项 二
3. 有序列表项 三


---
# <center>引用  
## 代码
```
引用需要在被引用的文本前加上>符号
> 这是一个有两段文字的引用,
> 无意义的占行文字1.
> 无意义的占行文字2.
> 
> 无意义的占行文字3.
> 无意义的占行文字4.

引用的多层嵌套：
>>> 请问 Markdwon 怎么用？ - 小白

>> 自己看教程！ - 愤青

> 教程在哪？ - 小白
```
## 显示效果
> 这是一个有两段文字的引用,
> 无意义的占行文字1.
> 无意义的占行文字2.
> 
> 无意义的占行文字3.
> 无意义的占行文字4.

>>> 请问 Markdwon 怎么用？ - 小白

>> 自己看教程！ - 愤青

> 教程在哪？ - 小白

---
# <center>表格  
## 代码
```
| Tables        | Are           | Cool  |
| ------------- |:-------------:| -----:|
| col 3 is      | right-aligned | $1600 |
| col 2 is      | centered      |   $12 |
| zebra stripes | are neat      |    $1 |
```
## 显示效果
| Tables        | Are           | Cool  |
| ------------- |:-------------:| -----:|
| col 3 is      | right-aligned | $1600 |
| col 2 is      | centered      |   $12 |
| zebra stripes | are neat      |    $1 |

---
# <center>流程图  
## 代码
> **Hexo可以调用[hexo-filter-flowchart](https://github.com/bubkoo/hexo-filter-flowchart)绘制流程图**

flow
st=>start: Start|past:>http://www.google.com[blank]
e=>end: End:>http://www.google.com
op1=>operation: My Operation|past
op2=>operation: Stuff|current
sub1=>subroutine: My Subroutine|invalid
cond=>condition: Yes
or No?|approved:>http://www.google.com
c2=>condition: Good idea|rejected
io=>inputoutput: catch something...|request

st->op1(right)->cond
cond(yes, right)->c2
cond(no)->sub1(left)->op1
c2(yes)->io->e
c2(no)->op2->e


## 显示效果

```flow
st=>start: Start|past:>http://www.google.com[blank]
e=>end: End:>http://www.google.com
op1=>operation: My Operation|past
op2=>operation: Stuff|current
sub1=>subroutine: My Subroutine|invalid
cond=>condition: Yes
or No?|approved:>http://www.google.com
c2=>condition: Good idea|rejected
io=>inputoutput: catch something...|request

st->op1(right)->cond
cond(yes, right)->c2
cond(no)->sub1(left)->op1
c2(yes)->io->e
c2(no)->op2->e
```


---
# <center>特殊字符  
## 代码
```
! &#33; — 惊叹号Exclamation mark 
” &#34; &quot; 双引号Quotation mark 
# &#35; — 数字标志Number sign 
$ &#36; — 美元标志Dollar sign 
% &#37; — 百分号Percent sign 
& &#38; &amp; Ampersand 
‘ &#39; — 单引号Apostrophe 
( &#40; — 小括号左边部分Left parenthesis 
) &#41; — 小括号右边部分Right parenthesis 
* &#42; — 星号Asterisk 
+ &#43; — 加号Plus sign 
< &#60; &lt; 小于号Less than 
= &#61; — 等于符号Equals sign 
> &#62; &gt; 大于号Greater than 
? &#63; — 问号Question mark 
@ &#64; — Commercial at 
[ &#91; --- 中括号左边部分Left square bracket 
\ &#92; --- 反斜杠Reverse solidus (backslash) 
] &#93; — 中括号右边部分Right square bracket 
{ &#123; — 大括号左边部分Left curly brace 
| &#124; — 竖线Vertical bar 
} &#125; — 大括号右边部分Right curly brace 
```
## 显示效果
特别注意的是小括号 ( ) 大括号 { } ,如果不小心写了,你执行hexo s –debug可能报一些莫名其妙的错误! 


---
# <center>其它
## 代码
```
<small>文本内容</small>
<!-- 注释 -->
分段：两个回车
换行：两个空格 + 回车
```
## 显示效果
<small>文本内容</small>
<!-- 注释 -->
