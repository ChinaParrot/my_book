# Django基本命令使用



  ##1. 新建一个 django project
  
  jqlinux_test是project名字，可以根据自己需求：
  
  
 ``` 
django-admin.py  startproject 
jqlinux_test
 
 ```
 
  
  ##2. 新建 app

<pre>python manage.py startapp app-name
或 django-admin.py startapp app-name

#一般一个项目有多个app, 当然通用的app也可以在多个项目中使用。

</pre>

例如：
<pre>
python manage.py startapp learn # learn 是一个app的名称

#查看文件列表：
learn/
├── admin.py
├── apps.py
├── __init__.py
├── migrations
│   └── __init__.py
├── models.py
├── tests.py
└── views.py

</pre>

把我们新定义的app加到settings.py中的INSTALL_APPS中

修改 mysite/mysite/settings.py
<pre>
INSTALLED_APPS = (
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
 
    'learn',
)
</pre>
备注,这一步是干什么呢? 新建的 app 如果不加到 INSTALL_APPS 中的话, django 就不能自动找到app中的模板文件(app-name/templates/下的文件)和静态文件(app-name/static/中的文件) , 后面你会学习到它们分别用来干什么.


##3. 同步数据库
  
<pre>python manage.py syncdb
#注意：Django 1.7.1及以上的版本需要用以下命令
python manage.py makemigrations
python manage.py migrate

#这种方法可以创建表，当你在models.py中新增了类时，运行它就可以自动在数据库中创建表了，不用手动创建。

备注：对已有的 models 进行修改，Django 1.7之前的版本的Django都是无法自动更改表结构的，不过有第三方工具 south,详见 Django 数据库迁移 一节。
 </pre>
  
  ##4. 使用开发服务器
  开发服务器，即开发时使用，一般修改代码后会自动重启，方便调试和开发，但是由于性能问题，建议只用来测试，不要用在生产环境。
 
 <pre>
 python manage.py runserver
 
# 当提示端口被占用的时候，可以用其它端口：
python manage.py runserver 8001
python manage.py runserver 9999
（当然也可以kill掉占用端口的进程）
 
# 监听所有可用 ip （电脑可能有一个或多个内网ip，一个或多个外网ip，即有多个ip地址）
python manage.py runserver 0.0.0.0:8000
# 如果是外网或者局域网电脑上可以用其它电脑查看开发服务器
# 访问对应的 ip加端口，比如 http://172.16.20.2:8000
 </pre>
  
  ##5. 清空数据库
  <pre>
  python manage.py flush
  #此命令会询问是 yes 还是 no, 选择 yes 会把数据全部清空掉，只留下空表。
  </pre>
  
  ##6. 创建超级管理员
  <pre>
  python manage.py createsuperuser
 
# 按照提示输入用户名和对应的密码就好了邮箱可以留空，用户名和密码必填
 
# 修改 用户密码可以用：
python manage.py changepassword username
  </pre>
  
  ##7. 导出数据 导入数据
  
  <pre>
python manage.py dumpdata appname > appname.json
python manage.py loaddata appname.json
  </pre>
  
  ##8. Django 项目环境终端
  
  <pre>
  python manage.py shell
  
#如果你安装了 bpython 或 ipython 会自动用它们的界面，推荐安装 bpython。
#这个命令和 直接运行 python 或 bpython 进入 shell 的区别是：你可以在这个 shell 里面调用当前项目的 models.py 中的 API，对于操作数据，还有一些小测试非常方便。
  </pre>
  
  
  ##9. 数据库命令行
  <pre>
  python manage.py dbshell
  #Django 会自动进入在settings.py中设置的数据库，如果是 MySQL 或 postgreSQL,会要求输入数据库用户密码。

#在这个终端可以执行数据库的SQL语句。如果您对SQL比较熟悉，可能喜欢这种方式。
  </pre>
  
  

###例子：hello world

<pre>
#1.创建一个mysite的项目
django-admin startproject mysite

#2.新建一个应用(app), 名称叫 learn
python manage.py startapp learn

#3.把我们新定义的app加到settings.py中的INSTALL_APPS中
修改 mysite/mysite/settings.py

INSTALLED_APPS = (
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
 
    'learn',
)

#我们在learn这个目录中,把views.py打开,修改其中的源代码,改成下面的
#coding:utf-8
from django.http import HttpResponse
 
def index(request):
    return HttpResponse(u"hello world!")
    
#定义视图函数相关的URL(网址)
 我们打开 mysite/mysite/urls.py 这个文件, 修改其中的代码:
 
 Django 1.8.x及以上，Django 官方鼓励（或说要求）先引入，再使用：

from django.conf.urls import url
from django.contrib import admin
from learn import views as learn_views  # new
 
urlpatterns = [
    url(r'^$', learn_views.index),  # new
    url(r'^admin/', admin.site.urls),
]
 
 python manage.py runserver 0.0.0.0:8080
 Performing system checks...

System check identified no issues (0 silenced).
May 25, 2016 - 06:24:45
Django version 1.11, using settings 'mysite.settings'
Starting development server at http://0.0.0.0:8080/
Quit the server with CONTROL-C.

</pre>

最后浏览器访问：http://ip:8080/
