# Django 配置settings.py详解

##1.DEBUG

DEBUG 配置为 True 的时候会暴露出一些出错信息或者配置信息以方便调试.但是在上线的时候应该将其关掉，防止配置信息或者敏感出错信息泄露.


```
DEBUG = False

```
##2.数据库连接配置从文件读取

* 通过 ConfigParser

```
import os
import ConfigParser
BASE_DIR = os.path.abspath(os.path.dirname(os.path.dirname(__file__)))
config = ConfigParser.ConfigParser()
config.read(os.path.join(BASE_DIR,'configue.conf'))

# DATABASES = {}
# if config.get('db', 'engine') == 'mysql':
#     DB_HOST = config.get('db', 'host')
#     DB_PORT = config.getint('db', 'port')
#     DB_USER = config.get('db', 'user')
#     DB_PASSWORD = config.get('db', 'password')
#     DB_DATABASE = config.get('db', 'database')
#     DATABASES = {
#         'default': {
#             'ENGINE': 'django.db.backends.mysql',
#             'NAME': DB_DATABASE,
#             'USER': DB_USER,
#             'PASSWORD': DB_PASSWORD,
#             'HOST': DB_HOST,
#             'PORT': DB_PORT,
#         }
#     }
# elif config.get('db', 'engine') == 'sqlite':
#     DATABASES = {
#         'default': {
#             'ENGINE': 'django.db.backends.sqlite3',
#             'NAME': config.get('db', 'database'),
#         }
#     }
# else:
#     DATABASES = {
#         'default': {
#             'ENGINE': 'django.db.backends.sqlite3',
#             'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),
#         }
# }

#配置文件
[db]
engine = mysql
host = 127.0.0.1
port = 3306
user = root
password = root
database = dragon
```



