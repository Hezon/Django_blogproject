1. 进入虚拟环境，安装 Python Markdown
```
pip install markdown
```
2. 在 detail 视图中渲染 Markdown
```
# blog/views.py

import markdown
...

def detail(request, pk):
    ...
    post.body = markdown.markdown(post.body,
                                  extensions=[
                                     'markdown.extensions.extra',
                                     'markdown.extensions.codehilite',
                                     'markdown.extensions.toc',
                                  ])
    ...
```
extra 本身包含很多拓展，而 codehilite 是语法高亮拓展，这为我们后面的实现代码高亮功能提供基础，而 toc 则允许我们自动生成目录
3. 在模板渲染{{post.body}}的地方添加safe
```
{{ post.body|safe }}
```
不加safe会出现html标签，这是因为Django 出于安全方面的考虑，任何的 HTML 代码在 Django 的模板中都会被转义。为了解除转义，只需在模板标签使用 safe 过滤器即可。
4. 激活虚拟环境，安装 Pygments（代码高亮）
```
pip install Pygments
```
Pygments 的工作原理是把代码切分成一个个单词，然后为这些单词添加 css 样式
5. 引入样式文件
```
# base.html
<link rel="stylesheet" href="{% static 'blog/css/highlights/github.css' %}">
```
