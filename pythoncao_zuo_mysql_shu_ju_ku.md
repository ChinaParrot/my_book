**Python操作mysql数据库**

**一、安装模块**

```
1、Ubuntu类环境

 apt-get install python-mysqldb 

2、源码安装：

下载地址： https://pypi.python.org/pypi/MySQL-python
 
unzip MySQL-python-1.2.5.zip
cd MySQL-python-1.2.5
python setup.py build
python setup.py install
 
```

**二、应用**

数据库连接

连接数据库前，请先确认以下事项： 

您已经创建了数据库 TESTDB. 

在TESTDB数据库中您已经创建了表 EMPLOYEE 

EMPLOYEE表字段为 FIRST\_NAME, LAST\_NAME, AGE, SEX 和 INCOME。 

连接数据库TESTDB使用的用户名为 "testuser" ，密码为 "test123",你可以可以自己设定或者直接使用root用户名及其密码，Mysql数据库用户授权请使用Grant命令。

在你的机子上已经安装了 Python MySQLdb 模块。

实例：

以下实例链接Mysql的TESTDB数据库：

```
#!/usr/bin/env python3
# -*- coding: UTF-8 -*-
import MySQLdb

# 打开数据库连接
db = MySQLdb.connect("localhost","testuser","test123","TESTDB" )

# 使用cursor()方法获取操作游标
cursor = db.cursor()

# 使用execute方法执行SQL语句
cursor.execute("SELECT VERSION()")

# 使用 fetchone() 方法获取一条数据库。
data = cursor.fetchone()

print ("Database version : %s " % data)

# 关闭数据库连接
db.close()
```



