## 输出变量值  

使用双花括号{{ variable_name }}来输出变量的值。

```bash
<p>Hello, {{ user.username }}!</p>
```

## 控制结构

使用模板标签（以{%和%}包围）来添加控制结构，如条件语句、循环和逻辑运算符。

```bash
{% if user.is_authenticated %}
  <p>Welcome, {{ user.username }}!</p>
{% else %}
  <p>Please log in to continue.</p>
{% endif %}
```

## 迭代列表

使用for标签来迭代列表中的元素。

```bash
<ul>
  {% for item in items %}
    <li>{{ item }}</li>
  {% endfor %}
</ul>
```

## 过滤器

使用管道符|来应用过滤器来修改变量的输出。

```bash
<p>{{ some_text|upper }}</p>
```
date过滤器：用于格式化日期和时间。
```bash
{{ some_date|date:"Y-m-d" }}
```
default过滤器：在变量值为空或不存在时提供默认值。
```bash
{{ variable|default:"No value" }}
```
length过滤器：返回列表或字符串的长度。
```bash
{{ some_list|length }}
```
truncatechars过滤器：将字符串截断为指定字符数。
```bash
{{ long_text|truncatechars:50 }}
```
lower和upper过滤器：将字符串转换为小写或大写。
```bash
{{ text|lower }}
{{ text|upper }}

```
slice过滤器：对列表或字符串进行切片操作。
```bash
{{ some_list|slice:":3" }}
{{ text|slice:"5:" }}
```
join过滤器：将列表的元素连接成一个字符串。
```bash
{{ some_list|join:", " }}
```
add过滤器：将变量与另一个值相加。
```bash
{{ number|add:5 }}
```
创建自定义过滤器函数：

```bash
# 在应用的templatetags目录下创建一个Python文件，例如custom_filters.py
from django import template

register = template.Library()

@register.filter(name='my_custom_filter')
def my_custom_filter(value, arg):
    # 在这里执行自定义过滤器的操作，使用value作为输入并返回结果
    result = value + arg
    return result

```
在模板中使用自定义过滤器：

```bash
{% load custom_filters %}

<p>{{ some_text|my_custom_filter:" additional text" }}</p>
```

## 静态文件

使用static标签来引用静态文件（如CSS、JavaScript）

```bash
<link rel="stylesheet" type="text/css" href="{% static 'css/style.css' %}">
```

## 继承和包含

使用extends和include标签来创建模板继承和包含其他模板。

基础模板（base.html）：

```bash
<!DOCTYPE html>
<html>
<head>
  <title>{% block title %}Default Title{% endblock %}</title>
</head>
<body>
  <div id="content">
    {% block content %}{% endblock %}
  </div>
</body>
</html>
```

子模板（child.html）：

```bash
{% extends "base.html" %}

{% block title %}Page Title{% endblock %}

{% block content %}
  <h1>Hello, World!</h1>
{% endblock %}
```



