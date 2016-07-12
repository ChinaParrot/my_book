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

