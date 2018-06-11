### 绑定 URL 与视图函数
1. blog 应用的目录下创建一个 urls.py 文件
2. 在 blog\urls.py 中写入这些代码：
```
from django.conf.urls import url

from . import views

urlpatterns = [
    url(r'^$', views.index, name='index'),
]
```

### 编写视图函数
在 blog\views.py 中写入这些代码：
```
from django.http import HttpResponse

def index(request):
    return HttpResponse("欢迎访问我的博客首页！")
```

### 配置项目 URL
在blogproject\urls.py中修改成如下的形式：
```
from django.conf.urls import url
from django.conf.urls import url, include
from django.contrib import admin

urlpatterns = [
    url(r'^admin/', admin.site.urls),
    url(r'', include('blog.urls')),
]
```

### 创建模板
1. 在根目录创建templates\blog\index.html
2. 在 templates\blog\index.html 文件里写入下面的代码：
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>{{ title }}</title>
</head>
<body>
<h1>{{ welcome }}</h1>
</body>
</html>
```
3. 在blogproject/settings.py写上
```
TEMPLATES = [
    {
        ...
        'DIRS': [os.path.join(BASE_DIR, 'templates')],
        ...
    },
]
```
4. 修改blog/views.py
```
from django.http import HttpResponse
from django.shortcuts import render

def index(request):
    return render(request, 'blog/index.html', context={
                      'title': '我的博客首页', 
                      'welcome': '欢迎访问我的博客首页'
                  })
```
