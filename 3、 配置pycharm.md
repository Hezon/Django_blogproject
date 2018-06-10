### 关联环境
1. 进入File>>Settings>>Project:django_blog>>Project Interpreter
2. 点击上面Project Interpreter右边的配置icon，选择show all
3. 选择添加
4. 选择Existing environment
5. 在Interpreter配置虚拟环境路径
```
C:\Users\jj728\workspace\env\blogproject_env\Scripts\python.exe
```


### 配置项目启动
1. 点击右上三角按钮左边的下拉框
2. 点击Edit Configurations
3. 点击Default
4. 点击Python
5. 配置Script Path，即项目manage.py的路径
```
C:\Users\jj728\workspace\pythonProject\blogproject\manage.py
```
6. 配置Parameters  

```
runserver 127.0.0.1:8080
```
7. 点击确定
8. 右击pychram工程目录下的manage.py文件，点击运行
9. 成功添加启动项