### 安装 Fabric
进入虚拟环境，并激活，安装Fabric3
```
pip install Fabric3
```

### 部署过程回顾
1. 远程连接服务器。
2. 进入项目根目录，从远程仓库拉取最新的代码。
3. 如果项目引入了新的依赖，需要执行 pip install -r requirement.txt 安装最新依赖。
4. 如果修改或新增了项目静态文件，需要执行 python manage.py collectstatic 收集静态文件。
5. 如果数据库发生了变化，需要执行 python manage.py migrate 迁移数据库。
6. 重启 Nginx 和 Gunicorn 使改动生效。


### 编写 Fabric 脚本
项目根目录，创建fabfile.py
```
from fabric.api import env, run
from fabric.operations import sudo

GIT_REPO = "you git repository" ① 

env.user = 'you host username' ②
env.password = 'you host password'

# 填写你自己的主机对应的域名
env.hosts = ['demo.zmrenwu.com']

# 一般情况下为 22 端口，如果非 22 端口请查看你的主机服务提供商提供的信息
env.port = '22'


def deploy():
    source_folder = '/home/yangxg/sites/zmrenwu.com/django-blog-tutorial' ③

    run('cd %s && git pull' % source_folder) ④
    run("""
        cd {} &&
        ../env/bin/pip install -r requirements.txt &&
        ../env/bin/python3 manage.py collectstatic --noinput &&
        ../env/bin/python3 manage.py migrate
        """.format(source_folder)) ⑤ 
    sudo('restart gunicorn-demo.zmrenwu.com') ⑥
    sudo('service nginx reload')
```


### 执行 Fabric 自动部署脚本
进入 fabfile.py 文件所在的目录
```
(blogproject_env) C:\Users\jj728\workspace\pythonProject\blogproject>fab deploy
```
