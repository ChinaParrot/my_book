 # MySQL安装

mysql官网地址：http://www.mysql.com/

##一、windows安装
###下载：

http://dev.mysql.com/downloads/mysql/

可以根据自己需求选择 mysql 5.5| mysql 5.6 |mysql 5.7

window 的mysql msi 安装版本只有32位。

例如下载5.7(64):

http://dev.mysql.com/get/Downloads/MySQL-5.7/mysql-5.7.13-winx64.zip

解压到：C:\mysql-5.7.13-winx64


###配置文件，创建 一个my.ini

```
[mysql]
default-character-set=utf8 

[mysqld]

skip-external-locking
skip-name-resolve
skip-networking
back_log = 600
server-id = 1
bind-address = 0.0.0.0

max_connections = 500
max_connect_errors = 500
#open_files_limit = 65535

port = 3306 
basedir = C:\mysql-5.7.13-winx64
datadir = C:\mysql-5.7.13-winx64\data
log_error = C:\mysql-5.7.13-winx64\log\mysql-error.log
slow_query_log = 1
long_query_time = 5
slow_query_log_file = C:\mysql-5.7.13-winx64\log\mysql-slow.log

port =3306 
character-set-server=utf8
join_buffer_size = 32M
sort_buffer_size = 1M
read_rnd_buffer_size = 1M 
read_buffer_size = 1M
key_buffer_size = 16M
default_storage_engine = InnoDB

sql_mode=NO_ENGINE_SUBSTITUTION,STRICT_TRANS_TABLES 

```

###安装
使用管理员用户登录cmd服务：

```

#操作如下：
cd c:\
cd mysql-5.7.13-winx64\bin

#安装服务
mysqld install MySQL --defaults-file="C:\mysql-5.7.13-winx64\my.ini" 

#如果移除服务
mysqld remove

#创建log日志目录
mkdir C:\mysql-5.7.13-winx64\log

#初始化数据（注意密码在错误日志里）
mysqld.exe --initialize

#启动mysql服务
net start mysql

#查看服务
netstat -ano | findstr "3306"

```


window常用：
 
 1. sc delete +服务删除服务
 2. netstat -ano | findstr "3306" #查询启动端口
 
 
 ##二、linux安装
 
 ###1.linux 二进制安装mysql
 cento系列：
 
 下载yum Repository:http://dev.mysql.com/downloads/repo/yum/
 
 Ubuntu系列：
 下载 apt:
 http://dev.mysql.com/downloads/repo/apt/
 
 yum | apt -y install mysql-server 
 
 ###2.linux 源码安装
 
 以centos为例：
 
 注意：建议安装mysql 5.6 ，mysql5.7需要更大的内存编译，否则不通过，至少2g内存。
 
```

#add mysql
id -u mysql >/dev/null 2>&1
[ $? -ne 0 ] && useradd -M -s /sbin/nologin mysql

#安装依赖：

 yum -y install gcc gcc-c++ cmake ncurses-devel openssl-devel bison libaio-devel libaio readline-devel readline
 
 #下载：
mkdir /tmp/mysql && cd /tmp/mysql
 wget http://dev.mysql.com/get/Downloads/MySQL-5.6/mysql-5.6.31.tar.gz
 
 #编译安装
 tar xvf mysql-5.6.31.tar.gz
 cd mysql-5.6.31

cmake . -DCMAKE_INSTALL_PREFIX=/opt/mysql \
-DMYSQL_DATADIR=/data/mysql \
-DSYSCONFDIR=/etc \
-DWITH_INNOBASE_STORAGE_ENGINE=1 \
-DWITH_PARTITION_STORAGE_ENGINE=1 \
-DWITH_FEDERATED_STORAGE_ENGINE=1 \
-DWITH_BLACKHOLE_STORAGE_ENGINE=1 \
-DWITH_MYISAM_STORAGE_ENGINE=1 \
-DENABLED_LOCAL_INFILE=1 \
-DENABLE_DTRACE=0 \
-DEXTRA_CHARSETS=all \
-DDEFAULT_CHARSET=utf8 \
-DDEFAULT_COLLATION=utf8_general_ci \
-DWITH_EMBEDDED_SERVER=1 \
-DWITH_SSL=system \
-DWITH_DEBUG=0 

make -j `grep processor /proc/cpuinfo | wc -l` && make install

#添加服务启动
/bin/cp ./support-files/mysql.server /etc/init.d/mysqld
chmod +x /etc/init.d/mysqld

#添加配置文件
mv /etc/my.cnf /etc/my.cnf.bak

#########################################
cat /etc/my.cnf  
[mysql]

# CLIENT #
port                           = 3306
socket                         = /data/mysql/mysql.sock

[mysqld]

# GENERAL #
user                           = mysql
default-storage-engine         = InnoDB
socket                         = /data/mysql/mysql.sock
pid-file                       = /data/mysql/mysql.pid

# MyISAM #
key-buffer-size                = 32M
myisam-recover                 = FORCE,BACKUP

# SAFETY #
max-allowed-packet             = 16M
max-connect-errors             = 1000000
skip-name-resolve
sql-mode                       = STRICT_TRANS_TABLES,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_AUTO_VALUE_ON_ZERO,NO_ENGINE_SUBSTITUTION,NO_ZERO_DATE,NO_ZERO_IN_DATE,ONLY_FULL_GROUP_BY
sysdate-is-now                 = 1
innodb                         = FORCE
innodb-strict-mode             = 1

# DATA STORAGE #
datadir                        = /data/mysql

# BINARY LOGGING #
log-bin                        = /data/mysql/mysql-bin
expire-logs-days               = 14
sync-binlog                    = 1

# CACHES AND LIMITS #
tmp-table-size                 = 32M
max-heap-table-size            = 32M
query-cache-type               = 0
query-cache-size               = 0
max-connections                = 500
thread-cache-size              = 50
open-files-limit               = 65535
table-definition-cache         = 1024
table-open-cache               = 2048

# INNODB #
innodb-flush-method            = O_DIRECT
innodb-log-files-in-group      = 2
innodb-log-file-size           = 64M
innodb-flush-log-at-trx-commit = 1
innodb-file-per-table          = 1
innodb-buffer-pool-size        = 592M

# LOGGING #
log-error                      = /data/mysql/mysql-error.log
log-queries-not-using-indexes  = 1
slow-query-log                 = 1
slow-query-log-file            = /data/mysql/mysql-slow.log
###################################################

#初始化数据库
./scripts/mysql_install_db --user=mysql --basedir=/opt/mysql --datadir=/data/mysql
chown mysql.mysql -R /data/mysql

 #启动服务
 /etc/init.d/mysqld start
 
 #修改密码以及删除不用的数据库和用户
 /opt/mysql/bin/mysql -e "grant all privileges on *.* to root@'127.0.0.1' identified by \"123456\" with grant option;"
/opt/mysql/bin/mysql -e "grant all privileges on *.* to root@'localhost' identified by \"123456\" with grant option;"
/opt/mysql/bin/mysql -uroot -p123456 -e "delete from mysql.user where Password='';"
/opt/mysql/bin/mysql -uroot -p123456 -e "delete from mysql.db where User='';"
/opt/mysql/bin/mysql -uroot -p123456 -e "delete from mysql.proxies_priv where Host!='localhost';"
/opt/mysql/bin/mysql -uroot -p123456 -e "drop database test;"
/opt/mysql/bin/mysql -uroot -p123456 -e "reset master;"
 
```
 
 或者脚本安装：

```
wget https://www.jqlinux.com/xjq/shell/mysql.sh
sh mysql.sh

```
