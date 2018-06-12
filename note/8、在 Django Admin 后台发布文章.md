1. 在 Admin 后台注册模型
```
# blog/admin.py

from django.contrib import admin
from .models import Post, Category, Tag

admin.site.register(Post)
admin.site.register(Category)
admin.site.register(Tag)
```

2. 在 http://127.0.0.1:8080/admin/ 登录后台，在Posts栏目点击添加。进入文章编辑页面。

3. 定制 Admin 后台
在 admin post 列表页面，我们只看到了文章的标题，但是我们希望它显示更加详细的信息，这需要我们来定制 Admin 了，在 admin.py 添加如下代码：
```
# blog/admin.py

from django.contrib import admin
from .models import Post, Category, Tag

class PostAdmin(admin.ModelAdmin):
    list_display = ['title', 'created_time', 'modified_time', 'category', 'author']

# 把新增的 PostAdmin 也注册进来
admin.site.register(Post, PostAdmin)
admin.site.register(Category)
admin.site.register(Tag)
```
让表头显示为中文
```
# blog/models.py
...
class Post(models.Model):
    title = models.CharField('标题', max_length=70)
    body = models.TextField()
    created_time = models.DateTimeField('创建时间')
    modified_time = models.DateTimeField('修改时间')
    excerpt = models.CharField(max_length=200, blank=True)
    category = models.ForeignKey(Category, verbose_name='类别')
    tags = models.ManyToManyField(Tag, blank=True)
    author = models.ForeignKey(User, verbose_name='作者')

    def __str__(self):
        return self.title

```
