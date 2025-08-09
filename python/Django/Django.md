## 0.项目始动

- pycharm 初始化项目
  - 使用 Django 初始化
- vscode 创建项目
  - 创建虚拟环境`python3 -m venv venv`
  - 进入虚拟环境`source venv/bin/activate`
  - 下载 Django`pip install django`
  - 使用 Django 初始化`django-admin startproject config .`
- setting.py 配置
  - 配置 black `pip install black`
  - 语言时区`LANGUAGE_CODE = "zh-hans" TIME_ZONE = "Asia/Shanghai"`
- 创建 APP`python3 manage.py startapp app_name`
  - 注意在 setting.py 中进行注册
- 创建数据库
  - 下载`mysqlclient` `pip install mysqlclient`
  - 在 setting.py 中进行数据库链接
- 创建超级管理员`python3 manage.py createsuperuser`

## 1. Django 搭建

- 创建 Django 项目

```
django-admin startproject pro_name

django-admin startproject pro_name .  # 将当前目录作为项目目录
```

```
mysite
	├── manage. py          「管理项目文件：运行、类自动生成数据表」
	└── mysite
	  ├── __init__.py
	  ├── settings.py       「项目配置文件：如数据库」
	  ├── urls.py           「根路由」
	  ├── asgi.py           「异步运行项目」 - 不进行修改
	  └── wsgi.py           「同步运行项目」 - 不进行修改
```

- 项目运行

```
python3 manage.py runserver
```

- 创建 APP，编写具体业务代码

```
python3 manage.py startapp app_name
```

```
app_name
    ├── __init__.py
    ├── admin.py          ［内部后台管理配置］ - 不进行修改
    ├── apps.py           ［APP名字］ - 不进行修改
    ├── migrations        ［迁移记录，默认生成］ - 不进行修改
       └── __init__.py
    ├── models.py         ［数据库，类->SQL语句（ORM）］
    ├── tests.py
	├── templates         ［模板文件］
	    └── index.html
	├── statics           ［静态文件］
		└── bootstrap-3.4.1
    └── views.py          ［视图函数，do_login］
```

## 2.MVT

![[Pasted image 20250613175557.png]]

## 3. 路由匹配(urls)

- 精确字符串
  - `path("hello/", app01.hello)`
- 路径转换器
  - `path("article/<int:year>", app01.article),`
  - 需要指定 year 的数据类型，有 str(默认可不写)、int、slag(标签)
  - 对应的模板函数，需要在形参中添加对应的变量`def article(request, year):`
- 正则表达式
  - `re_path(r"^article/(?P<year>[0-9]{4})/(?P<month>[0-9]{2})$", app01.article_month),`

## 4. 视图函数(Views)

```python
from django.shortcuts import render, redirect, HttpResponse
from django.views import View


# 函数视图
def login(request):

	# 业务代码：如用户登录 - 连接数据库进行校验

    return HttpResponse('欢迎光临~')

# 类视图
class LoginView(View):
	def get(self, request):
		return render(request, "login.html")

	def post(self, request):
		user_name = request.POST.get("username")
		password = request.POST.get("password")
		return HttpResponse(f"user_name:{user_name}, password: {password}")
```

- 函数视图
  - `request`
    - 包含用户所发送的请求数据，包括 URL 数据、post 请求体数据等
  - 返回值
    - 文本值：`return HttpResponse('欢迎光临~')`
    - 页面模板：`return render(request, 'index.html')`
      - **需要在 `setting.py` 中的 `INSTALLED_APPS` 进行 APP 注册**
    - 页面跳转：`return redirect('www.baidu.com')`
- 类视图
  - 在 url 中使用时，需要`path("register/", views.RegisterView.as_view()),`
  - 通用视图
- 请求信息（HttpRequest）
  - 请求头，可以通过`request.META`、`request.header`获取
    - 如获取`user-agent`判断是否为爬虫
    - 获取 IP 地址判断是否频繁访问
  - 请求参数
    - GET、URL 参数
      - `request.GET.get('arg_name', default_value)`
    - POST 参数
      - `request.POST.get('arg_name', default_value)`
    - 路径参数
      - 如`http://127.0.0.1:8000/article/2002/08`
      - 在函数的形参中传入`def article(request, year):`
    - 请求体中的 JSON
      - `data = json.load(request.body)`
- 响应信息(HttpResponse)
  - HttpResponse
  - JsonResponse

## 5.模板函数(Templates)

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Title</title>
    <link
      rel="stylesheet"
      href="{ % static 'bootstrap-3.4.1/css/bootstrap.min.css' % }"
    />
  </head>
  <body>
    <p>Hello World!</p>

    <ul>
      {% for item in data_list %}
      <li>{{ item }}</li>
      {% endfor %}
    </ul>
  </body>
</html>
```

- `static`
  - 通过在`setting.py`文件中配置`STATIC_URL`，可以统一管理所有的静态文件存放目录
- 继承
  - 不重要，略过

## 6.ORM(对象关系映射)（Models）

- 创建数据库链接

```python
# setting.py
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',  # 修改成MySQL数据库
        'NAME': 'Django',  # 连接数据库名称 先创建好才能指定
        'USER': 'root',  # 数据库名称
        'PASSWORD': 'pyz6znurk',  # 数据库密码
        'HOST': '127.0.0.1',  # 数据库ip 本地回环地址
        'PORT': 3306,  # 数据库端口
        'CHARSET': 'utf8'  # 指定字符编码
    }
}
```

- 在 models.py 文件中进行 models 的编写

```python
from django.db import models


class UserInfo(models.Model):
    name = models.CharField(verbose_name='姓名', max_length=16)  # varchar(16)
    age = models.IntegerField(verbose_name='年龄')  # integer
    email = models.CharField(verbose_name='邮箱', max_length=32)


class Department(models.Model):
    title = models.CharField(verbose_name='部门名称', max_length=60)
    count = models.IntegerField(verbose_name='人数')

	# 元数据
	class Meta:
		db_table = "department"
		verbose_name = "部门表"
```

- **使用如下命令，生成数据库**
  - 需要使用`mysqlclient`依赖
  - `pip install mysqlclient`

```shell
python3 manage.py makemigrations # 读取所有已注册的APP的models.py文件，生成配置文件并存放在对应APP的migrations目录下
python3 manage.py migrate # 根据migrations的最新配置文件，生成SQL语句
```

- 字段类型
  ![[Pasted image 20250613222656.png]]
  ![[Pasted image 20250613222801.png]]
- 数据操作 CRUD
  - 查询条件
    - `id__gt`：大于
    - `id__gte`：大于等于
    - `id__lt`：小于
    - `id__lte`：小于等于
    - `id__isnull`：是否为空
    - `username__contains=='an'`：用户名中包含 an 的数据项
    - `username__icontains=='an'`：用户名中包含 an 的数据项，不区分大小写
    - `id__in==[1,2,3]`：id 落入某一列表的数据项
    - `username__startswith=='a'`：用户名以 a 开头
    - `username__endswith=='a'`：用户名以 a 结尾
    - 日期和时间`created_at__year==2022`
  - Q 函数：多条件联查

```python
from web import models

# 新增
models.Department.objects.create(title='就业部', count=1200)

# 查询
query_set = models.Department.objects.filter(count__gt=15) # 查询所有count大于15的数据项
query_set = models.Department.objects.all() # 全查
obj = models.Department.objects.all().first() # 返回第一条数据 last()为最后一条数据
query_set = models.Department.objects.all().order('id') # 排序 ('id')正序/('-id')倒序

# 删除
# 软删除：在表中添加字段，为0时代表逻辑删除，查询时不显示
models.Department.objects.all().first().delete() # 硬删除

# 修改
models.Department.objects.filter(id=1).update(count=13)
```

- 基础 model 模板
  - 一般放在项目根目录下的 utils 文件夹内

```python
from django.db import models

# Create your models here.
class BaseModel(models.Model):
	created_at = models.DateTimeField(auto_now_add=True, verbose_name="创建时间")
	updated_at = models.DateTimeField(auto_now=True, verbose_name="更新时间")

	class Meta:
		abstract = True # 抽象类
```

- 创建超级管理员
  `python3 manage.py createsuperuser`

## 7.开发细节

- 富文本编辑器 ckeditor

```py
# shell中下载
pip install django-ckeditor

# 在setting.py中进行注册和路径配置
INSTALLED_APPS = [
	...
	'ckeditor',
	'ckeditor_uploader',
]
CKEDITOR_UPLOAD_PATH = "uploads/" # CKEditor 上传文件存储目录
CKEDITOR_IMAGE_BACKEND = "pillow" # 使用 Pillow 处理图片

# 注册路由 在config的urls.py中进行注册
urlpatterns = [
	...
	path("ckeditor/", include("ckeditor_uploader.urls")),
]

# 在models中使用
from ckeditor.fields import RichTextField # 富文本
from ckeditor_uploader.fields import RichTextUploadingField # 可以上传图片的富文本编辑器
```

- restful API
  - GET 获取资源
  - PUT 更新资源
  - POST 新建资源
  - DELETE 删除资源
- 序列化
  - 将 querySet 格式数据快速转化为 JSON 格式的数据

```py
# 安装插件
pip install djangorestframework

# 在setting.py中进行注册和路径配置
INSTALLED_APPS = [
	'rest_framework', # 添加 Django REST framework
]

# 使用序列化器 快捷进行JSON序列化操作
# 创建serializers.py文件并进行编写
from rest_framework import serializers
from .models import Movie

class MovieSerializer(serializers.ModelSerializer):
	class Meta:
		model = Movie
		fields = ['movie_name', 'release_year', 'director', 'scriptwriter',]

# 在view.py中，就可以使用序列化器对数据进行序列化
from django.shortcuts import render, HttpResponse
from rest_framework.views import APIView
from django.http import JsonResponse
from .models import Movie
from .serializers import MovieSerializer

class MovieList(APIView):
	def get(self, request):
		movies = Movie.objects.all()
		data = MovieSerializer(movies, many=True).data
		return JsonResponse(data, safe=False)

# 也可以使用generics组合视图快速开发接口
from rest_framework import generics
from .models import Movie
from .serializers import MovieSerializer, MovieDetailSerializer

class MovieList(generics.ListCreateAPIView):
	queryset = Movie.objects.all()
	serializer_class = MovieSerializer

class MovieDetail(generics.RetrieveUpdateDestroyAPIView):
	queryset = Movie.objects.all()
	serializer_class = MovieDetailSerializer
```

- viewSet 视图集使用

```py
# config的urls.py
from django.contrib import admin
from django.urls import path, include
from rest_framework import routers
from movie import views

routers = routers.DefaultRouter()
routers.register(r"movies", views.MovieList, basename="movies")

urlpatterns = [
	path("admin/", admin.site.urls),
	path("api/", include(routers.urls)),
]

# movie的view.py中
from rest_framework import viewsets
from .models import Movie
from .serializers import MovieSerializer

class MovieList(viewsets.ModelViewSet):
	queryset = Movie.objects.all()
	serializer_class = MovieSerializer
```
