## 创建项目

### cmd

```py
mkdir django_intro
django-admin startproject test1

```



### Pycharm

#### 查看pytho安装路径

```py
py -0p 
C:\Users\Lenovo\AppData\Local\Programs\Python\Python311\Scripts>
```

打开终端

Alt+F12

#### 创建app

```py
python manage.py startapp [app的名字]
```

#### 命令行启动

```py
python manage.py runserver
```

### Diango框架

>urls.py-->views.py-->templates(html)
>
>​	views.py的render函数替换(html)文件
>
>urls.py<--views.py<--templates
>
>​	urls.py把修改完的(html)数据传给浏览器