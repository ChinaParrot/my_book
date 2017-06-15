# python之ConfigParser读取配置文件

dragon.conf配置文件

```
[db]
host = 127.0.0.1
port = 3306
user = dragon
password = dragon
database = dragon

[mail]
mail_enable = 1
email_host = 
email_port = 587
email_host_user = 
email_host_password = 
email_use_tls = True
email_use_ssl = False

[connect]
nav_sort_by = ip
```

例子：

```
#-*- coding:UTF-8 -*-
'''
Created on 2016年6月14日

@author: xuejq
'''

import ConfigParser

conf = ConfigParser.ConfigParser()
conf.read("dragon.conf")
#conf.readfp("D:\python_develop_environment\workspace\dragon\src", "dragon.conf")

#获取指定的section，指定的option的值
host = conf.get("db", "host")
print host
port = conf.get("db","port")
print port

#获取所有的section
sections = conf.sections()
print sections

#写配置文件
# 更新指定section, option的值
conf.set("db","port","3307")

# 写入指定section, 增加新option的值
conf.set("db", "test", "test")

#添加新的section
conf.add_section("test")
conf.set("test", "test", "test")


#写到配置文件
conf.write(open("dragon.conf","w"))
```



