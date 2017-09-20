1、首先授权：

```
例如：
grant replication slave on *.* to replication@’%’identified by ‘123456’;
```

2、修改配置文件my.cnf

```
[mysqld]
# BINARY LOGGING #
server-id = 1 #从2，一般以IP结尾配置
log-bin = /data/mysql/mysql-bin 
expire-logs-days = 14
sync-binlog = 1
slave-net-timeout = 60#从不设置
#binlog-ignore-db = mysql
#从relay_log = relay-bin #开启中继日志 (日志存储位置尽量不要同数据存储同一磁盘同一目录，这里测试方便不重新指向)

```

3、主库锁表备份

```
 #锁表
 flush tables with read lock;
 #查看主数据库的状态(并记录下File字段和Position字段的值，在配置从服务器时有用到)
 show master status;
 #全部备份
 mysqldump -uroot -p -h127.0.0.1 -P3306 --all-databases --triggers --routines --events >>/mnt/windows/all.sql

 #解除锁表
 unlock tables;
```

4、从导入数据并配置主从

```
#导入数据
 mysql -uroot -p -h127.0.0.1 -P3306 < /mnt/windows/all.sql
#配置主从

 change master to master_host=’192.168.19.158′, master_port=3306 ,master_user=’replication’ , master_password=’123456′ ,master_log_file=’mysql-bin.000004′ ,master_log_pos=404;
 start slave;
 #查看同步情况
 show slave status \G
 Slave_IO_Running: Yes
 Slave_SQL_Running: Yes
```



