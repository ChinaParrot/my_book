# Django路由系统

 简而言之，django的路由系统作用就是使views里面处理数据的函数与请求的url建立映射关系。使请求到来之后，根据urls.py里的关系条目，去查找到与请求对应的处理方法，从而返回给客户端http页面数据。
 
 ![](django_router_01.jpg)
 
##一、最基础的url映射
<pre>
from django.conf.urls import patterns, include, url

from django.contrib import admin
admin.autodiscover()
from apptest import views

urlpatterns = patterns('',
    url(r'^admin/', include(admin.site.urls)),
    url(r'^index/$', views.index),
)

</pre>

1. 先从创建的app下的views.py面定义处理数据的函数

2. 在urls.py里导入views

3. 在urlpatterns里写入一条url与处理函数的l映射关系

4. url映射一般是一条正则表达式，“^” 字符串的开始，“$“ 字符串的结束

5. 当写成”^$“时，不输入任何url时不会在返回黄页，而是返回后面函数里对应的页面。一般这一条会写在url的最后。如：


