1. 激活虚拟环境
2. 切换到工程根目录下
```
manage.py makemigrations
```

```
manage.py migrate
```

---

其他：可在settings配置数据库，以下为默认数据库配置
```
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),
    }
}
```
