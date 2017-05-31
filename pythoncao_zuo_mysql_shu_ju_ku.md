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

执行以上脚本输出结果如下：

```
Database version : 5.0.45
```

**创建数据库表**

如果数据库连接存在我们可以使用execute\(\)方法来为数据库创建表，如下所示创建表EMPLOYEE：

```
#!/usr/bin/env python3
# -*- coding: UTF-8 -*-
import MySQLdb

# 打开数据库连接
db = MySQLdb.connect("localhost","testuser","test123","TESTDB" )

# 使用cursor()方法获取操作游标
cursor = db.cursor()

# 如果数据表已经存在使用 execute() 方法删除表。
cursor.execute("DROP TABLE IF EXISTS EMPLOYEE")

# 创建数据表SQL语句
sql = """CREATE TABLE EMPLOYEE (
FIRST_NAME CHAR(20) NOT NULL,
LAST_NAME CHAR(20),
AGE INT,
SEX CHAR(1),
INCOME FLOAT )"""

cursor.execute(sql)

# 关闭数据库连接
db.close()
```

**数据库插入操作**

以下实例使用执行 SQL INSERT 语句向表 EMPLOYEE 插入记录：

```
#!/usr/bin/env python3
# -*- coding: UTF-8 -*-
import MySQLdb

# 打开数据库连接
db = MySQLdb.connect("localhost","testuser","test123","TESTDB" )

# 使用cursor()方法获取操作游标
cursor = db.cursor()

# SQL 插入语句
sql = """INSERT INTO EMPLOYEE(FIRST_NAME,
LAST_NAME, AGE, SEX, INCOME)
VALUES ('Mac', 'Mohan', 20, 'M', 2000)"""
try:
    # 执行sql语句
    cursor.execute(sql)
    # 提交到数据库执行
    db.commit()
    # 自增id
    print (cursor.lastrowid)
except:
    # Rollback in case there is any error
    db.rollback()

# 关闭数据库连接
db.close()
```

以上例子也可以写成如下形式：

```
#!/usr/bin/env python
# -*- coding: UTF-8 -*-
import MySQLdb

# 打开数据库连接
db = MySQLdb.connect("localhost","testuser","test123","TESTDB" )

# 使用cursor()方法获取操作游标
cursor = db.cursor()

# SQL 插入语句
sql = "INSERT INTO EMPLOYEE(FIRST_NAME, \
LAST_NAME, AGE, SEX, INCOME) \
VALUES ('%s', '%s', '%d', '%c', '%d' )" % \
('Mac', 'Mohan', 20, 'M', 2000)
try:
    # 执行sql语句
    cursor.execute(sql)
    # 提交到数据库执行
    db.commit()
except:
    # 发生错误时回滚
    db.rollback()

# 关闭数据库连接
db.close()
```

实例：

以下代码使用变量向SQL语句中传递参数:

```
..................................

user_id = "test123"
password = "password"

con.execute('insert into Login values("%s", "%s")' % \
(user_id, password))
..................................
```

**数据库查询操作**

Python查询Mysql使用 fetchone\(\) 方法获取单条数据, 使用fetchall\(\) 方法获取多条数据。

fetchone\(\): 该方法获取下一个查询结果集。结果集是一个对象

fetchall\(\):接收全部的返回结果行.

rowcount: 这是一个只读属性，并返回执行execute\(\)方法后影响的行数。

实例：

查询EMPLOYEE表中salary（工资）字段大于1000的所有数据：

```
#!/usr/bin/env python3
# -*- coding: UTF-8 -*-

import MySQLdb

# 打开数据库连接
db = MySQLdb.connect("localhost","testuser","test123","TESTDB" )

# 使用cursor()方法获取操作游标
cursor = db.cursor()

# SQL 查询语句
sql = "SELECT * FROM EMPLOYEE \
WHERE INCOME > '%d'" % (1000)
try:
    # 执行SQL语句
    cursor.execute(sql)
    # 获取所有记录列表
    results = cursor.fetchall()
    for row in results:
        fname = row[0]
        lname = row[1]
        age = row[2]
        sex = row[3]
        income = row[4]
        # 打印结果
        print ("fname=%s,lname=%s,age=%d,sex=%s,income=%d" % \
(fname, lname, age, sex, income ))
except:
        print ("Error: unable to fecth data")

# 关闭数据库连接
db.close()
```



