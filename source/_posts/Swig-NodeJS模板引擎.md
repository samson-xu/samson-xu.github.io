---
title: Swig-NodeJS模板引擎
date: 2017-07-12 17:11:15
tags:
- Swig
categories:
- Web
- JavaScript
comments:
---

# 简介
&emsp;&emsp;swig 是node端的一个优秀简洁的模板引擎，类似Python模板引擎Jinja，目前不仅在node端较为通用，相对于jade、ejs优秀，而且在浏览器端也可以很好地运行。

# 特性
> * 支持大多数主流浏览器。

> * 表达式兼容性好。

> * 面向对象的模板继承。

> * 将过滤器和转换应用到模板中的输出。

> * 可根据路劲渲染页面。

> * 支持页面复用。

> * 支持动态页面。

> * 可扩展、可定制。

# 使用示例

## swig代码
``` swig
<h1>{{ pagename|title }}</h1>
<ul>
{% for author in authors %}
    <li{% if loop.first %} class="first"{% endif %}>{{ author }}</li>
{% endfor %}
</ul>
```

## JavaScript代码
``` js
var swig  = require('swig');
var template = swig.compileFile('/absolute/path/to/template.html');
var output = template({
    pagename: 'awesome people',
    authors: ['Paul', 'Jim', 'Jane']
});
```

## HTML输出代码
``` html
<h1>Awesome People</h1>
<ul>
    <li class="first">Paul</li>
    <li>Jim</li>
    <li>Jane</li>
</ul>
```