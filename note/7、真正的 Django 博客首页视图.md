1. 编写首页视图函数
```
# blog/views.py
from django.shortcuts import render
from .models import Post

def index(request):
    post_list = Post.objects.all().order_by('-created_time')
    return render(request, 'blog/index.html', context={'post_list': post_list})
```
2. 引入首页模板及css、js
3. 在settings配置写入
```
...
STATICFILES_DIRS = [ os.path.join(BASE_DIR, 'static')]
```
