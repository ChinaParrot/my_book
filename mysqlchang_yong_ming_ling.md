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

## mysql 对数据库授权

