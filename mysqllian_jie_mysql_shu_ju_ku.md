# mysql:连接Mysql数据库

mysql命令用户连接数据库。

mysql命令格式： mysql -h主机地址 -u用户名 －p用户密码

## 连接到本机上的MYSQL
首先打开DOS窗口，然后进入目录mysql\bin，再键入命令mysql -u root -p，回车后提示你输密码。

注意用户名前可以有空格也可以没有空格，但是密码前必须没有空格，否则让你重新输入密码。

如果刚安装好MYSQL，超级用户root是没有密码的，故直接回车即可进入到MYSQL中了，MYSQL的提示符是： mysql>

## 连接到远程主机上的MYSQL
假设远程主机的IP为：110.110.110.110，用户名为root，密码为abcd123。则键入以下命令：
    mysql -h110.110.110.110 -u root -p 123;（注：u与root之间可以不用加空格，其它也一样）

## 退出MYSQL命令
exit （回车）
