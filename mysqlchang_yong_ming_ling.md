# MySQL常用命令

####1. 检查mysql是否启动

```ps -ef | grep mysqld```

####2. 使用命令启动mysql
<pre>
#进入mysql安装目录
./bin/mysqld_safe &

</pre>

####3.如果你想关闭目前运行的 MySQL 服务器

<pre>
#进入mysql安装目录
./bin/mysqladmin -u root -p shutdown
Enter password: ******

</pre>

####4.mysql备份

<pre>
#备份所有数据库
mysqldump -h{ip} -u {user} -p{password} --all-databases(或者 -A ) >all_databases.sql

#备份某个或几个数据库
mysqldump -h{ip} -u{user} -p{password} --databases(或者 -B) 数据库1 数据库2 >xxx_databases.sql

#备份某个库一张或者多张表
mysqldump -h{ip} -u{user} -p{password} 数据库xx 表01 表02 

#导出全部表空间
mysqldump -h{ip} -u{user} -p{password} --all-databases --all-tablespaces 

#不导出任何表空间信息
mysqldump -h{ip} -u{user} -p{password} --all-databases --no-tablespaces 

#备份数据库中在数据库创建前，添加drop库语句
mysqldump -h{ip} -u{user} -p{password} --all-databases --add-drop-database 

#备份数据库中在创建表前，添加drop表语句
mysqldump -h{ip} -u{user} -p{password} --all-databases --add-drop-table (默认添加)
#去掉drop表
--skip-add-drop-table

#在每个表导出之前 lock tables 并之后unlock table(默认是打开状态，使用--skip-add-locks取消选项)

mysqldump [option] --all-datases --add-locks 

#只导出表结构不导出数据
mysqldump [option] --opt -d 数据库名

#只导出数据不导出表结构
mysqldump [option] -t 数据库名 

#导出特定的表结构
mysqldump [option] -B数据库名 --table 表名

#导出数据库中忽略sql错误
--force
</pre>

####5.mysql 对数据库授权
* 授权语句如下
<pre>
GRANT 权限 ON  数据库权限.表的权限范围  TO '用户名'@'权限ip' identified by '设置密码';
#刷新权限,不然不生效
flush privileges;
</pre>

* 权限列表

|权限| 权限级别| 权限说明|
|-|-|-|
|CREATE|数据库、表或索引|创建数据库、表或索引权限 |
|DROP|数据库或表|删除数据库或表权限|
|GRANT OPTION|数据库、表或保存的程序|赋予权限选项|
|REFERENCES|数据库或表||
|ALTER|表|更改表，比如添加字段、索引等|
|DELETE|表|删除数据权限|
|INDEX|表|索引权限|
|INSERT|表|插入权限|
|SELECT|表|查询权限|
|UPDATE|表|更新权限|
|CREATE VIEW|视图|创建视图权限|
|SHOW VIEW|视图|查看视图权限|
|ALTER ROUTINE|存储过程|更改存储过程权限|
|CREATE ROUTINE|存储过程|创建存储过程权限|
|EXECUTE|存储过程|执行存储过程权限|
|FILE|服务器主机上的文件访问|文件访问权限|
|CREATE TEMPORARY TABLES|服务器管理|创建临时表权限|
|LOCK TABLES|服务器管理|锁表权限|
|CREATE USER|服务器管理|创建用户权限|
|PROCESS|服务器管理|查看进程权限|
|RELOAD|服务器管理|执行flush-hosts, flush-logs, flush-privileges, flush-status, flush-tables, flush-threads, refresh, reload等命令的权限|
|REPLICATION CLIENT|服务器管理|复制权限|
|REPLICATION SLAVE|服务器管理|复制权限|
|SHOW DATABASES|服务器管理|查看数据库权限|
|SHUTDOWN|服务器管理|关闭数据库权限|
|SUPER|服务器管理|执行kill线程权限|
|CREATE USER|服务器管理|创建数据库用户的权限|
|TRIGGER|服务器管理|触发器权限|

* 查看权限

<pre>
#查看当前用户的权限：
show grants;

#查看某个用户的权限：
 show grants for '用户'@'授权服务器ip';

#回收权限
revoke delete on *.* from '用户'@'授权服务器ip';


#删除用户
#先查看用户
select host,user,password from user;
#删除
drop user '用户'@'授权服务器ip';

#对账户重命名
rename user 'jack'@'%' to 'jim'@'%';

#修改密码
SET PASSWORD FOR 'root'@'localhost' = PASSWORD('123456');
#或者
mysqladmin -uroot -p123456 password 1234abcd
#或者
use mysql
update user set PASSWORD = PASSWORD('1234abcd') where user = 'root';
#在丢失root密码的时候(mysql 小于等于5.6之前版本)
#启动
mysqld_safe --skip-grant-tables &
#无密码登录
mysql -u root
use mysql
update user set password = PASSWORD('123456') where user = 'root';
</pre>
