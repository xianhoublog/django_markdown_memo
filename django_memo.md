# django 模板之——变量相关语法



## ## 项目地址

C:\lswb\django\django20\django2.0-course-master\blog_20
http://127.0.0.1:8000/t_test/

[video address](https://ke.qq.com/webcourse/index.html#cid=431861&term_id=100515714&taid=3750696155780853&vid=5285890792372560871)

```java


// django 模板语言
常用语法：
{{}} 和 {% %}
变量相关 {{}}
逻辑相关的用 {% %}

1. 变量
	{{ name }}
2. for 循环
	{% for in book_list %}
		{{ forloop.counter }}
        {{ forloop.last}}
		{{ i }}
    {% endfor %}
3.if 判断
    {% if 10>5 %}
    ...
    {% else %}
    ...
    {% endif %}
4. if ... in 判断
    {% if name in name_list %}
     ...
    {% endif %}

```



## view.py

```python
# 测试用类
class Person:
    def __init__(self,name,salary):
        self.name = name
        self.salary = salary

    def run(self):
        return '今天好开心，跑了三米'

    def __str__(self):
        return '<Person-object {}>'.format(self.name)
#模板语言测试相关
def template_test(request):
    name_list = ['张三','李四','王五']
    name_dict = {'name1':'小黑','name2':'长江','name3':'诸葛亮'}
    p1 = Person('小白',9000)
    p2 = Person('小黑',10000)
    p_list = [p1,p2]
    return render(
        request,
        't_test.html',
        {
            'name':'nannan',
            'age':18,
            'name_list':name_list,
            'name_dict': name_dict,
            'p1':p1,
            'p2':p2,
            'p_list':p_list
        }
    )
```



## t_test.html



```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<h1>模板语言测试页面</h1>
{{ name }} {{ age }} {{ notexist}}
<hr>
{{ name_list }}
<ul>
    {% for name in name_list %}
         <li>
             {{name }}
        </li>
    {% endfor %}

</ul>
{{ name_list.0 }}

<hr>
{{ name_dict }}
{{ name_dict.name1}}
    
    

<hr>
{{ p1 }}
{{ p1.name }} {{ p1.salary }}
{{ p1.run }}

<hr>
{{ p_list }}
{{ p_list.1.name}}
</body>
</html>
```



## url.py

```python
 path('t_test/', blog.views.template_test), # 模板语言测试
```



# Django 模板语言之——Filter

## 语法: {{ value:default: "nothing" }}

如果value值没有传的话就显示nothing

## length

{{ value|length }}

'|' 左右没有空格没有空格没有空格



## filesizeformat

```html
<p>文件大小： {{ file_size|filesizeformat}}</p>
```

## slice

```python 
切片
{{ value|slice:"2:-1"}}

<p>切片： {{ name_dict.name3|slice:"1:-1"}}</p>
```

## date

格式化

```html
<p>时间格式化：{{ now|date:"Y-m-d H:i:s"}}</p>
```

```python
from datetime import datetime
    now = datetime.now()
```

## safe

过滤器safe告诉Django这段代码是安全的不必转义

```html
<p>a标签 {{ a_html|safe }}</p>
<p>script标签 </p>
{{ script_html|safe }}
```

```python
 a_html = "<a href='http://www.baidu.com'> 我是后端传过来的a标签</a>"
    script_html = "<script> for(var i=0; i<3; i++){alert(123);} </script>"
```

## truncatechars

如果字符串字符多于指定的字符数量， 那么会被截断。 截断的字符串将以可翻译的省率号序列("...")结尾

##  自定义filter

自定义过滤器只是带有一个或两个参数的python函数

- 变量（输入）的值-- 不一定是一个字符串

- 参数的值 - 可以有一个默认值，或者完全省略

  ### 编写自定义filter

  templatetags\myfilter.py 

```python
from django import template
register = template.Library()

@register.filter(name="sb")
def add_sb(arg):
    return "{} sb.".format(arg)

@register.filter(name="addstr")
def add_str(arg, arg2):
    return "{} {}.".format(arg, arg2)
```



### 使用阶段

```html
<p>自定义filter方法</p>
{% load myfilter %} # 引入刚才py文件
{{ name|sb }} # 不加额外参数的方法
{{name_list.0|sb }}

{{name|addstr:"牛"}} # 添加额外的参数的方法
```

# Django 模板语言之——tags

### for 循环可用的一些参数：

| Variable            | Description                          |
| ------------------- | ------------------------------------ |
| forloop.counter     | 当前循环的索引值（从1开始）          |
| forloop.counter0    | 当前循环的索引值（从0开始）          |
| forloop.revcounter  | 当前循环的倒序索引值（从1开始）      |
| forloop.revcounter0 | 当前循环的倒序索引值（从0开始）      |
| forloop.first       | 当前循环是不是第一次循环（布尔值）   |
| forloop.last        | 当前循环是不是最后一次循环（布尔值） |
| forloop.parentloop  | 本层循环的外层循环                   |



### for... empty...

```html
{% for i in all_book %}
	<tr>
        <td>{{ forloop.counter}}</td>
         <td>{{ i.id}}</td>
         <td>{{ i.title}}</td>
	</tr>
{% empty %}
	<tr>
        <td colspan="5" class="text-center">暂时没有数据</td>
	</tr>
{% endfor %}
```



### if,elif 和 else

```html

<p> if elif else</p>
{% if p3 %}
<p>p3:{{ p3 }}</p>
{% elif p2 %}
<p>p2:{{ p2 }}</p>
{% else %}
<p>nobody!</p>
{% endif %}
```

当然也可以只有if 和else

```html
{% if name_list|length >=3 %}
    <p>需要打两辆车</p>
{% else %}
    <p>需要打一辆车</p>
{% endif %}
```



if 语句支持and, or, ==, >, <, !=, <=, >=, in , not in , is , is not 判断





### width

​	定义一个中间变量

```html
{% with name=name_list2.1.1 %}
 {{name}}
{% endwith %}

```



### 注释

