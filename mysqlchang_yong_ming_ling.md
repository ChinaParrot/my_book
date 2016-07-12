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


#导出全部表空间
mysqldump -h{ip} -u{user} -p{password} --all-databases --all-tablespaces 

</pre>