# 一、文件基本属性
Linux系统是一种典型的多用户系统，不同的用户处于不同的地位，拥有不同的权限。为了保护系统的安全性，Linux系统对不同的用户访问同一文件（包括目录文件）的权限做了不同的规定。在Linux中我们可以使用ll或者ls –l命令来显示一个文件的属性以及文件所属的用户和组，如：


```
[root@bogon ~]# ll /
total 94
dr-xr-xr-x.   2 root root  4096 Apr 18 14:05 bin
dr-xr-xr-x.   5 root root  1024 Apr 18 14:07 boot
drwxr-xr-x   16 root root  3600 Apr 19 16:41 dev
drwxr-xr-x.  69 root root  4096 Apr 19 14:13 etc
drwxr-xr-x.   3 root root  4096 Apr 19 14:10 home
dr-xr-xr-x.   8 root root  4096 Apr 18 14:05 lib
dr-xr-xr-x.   9 root root 12288 Apr 18 14:06 lib64
drwx------.   2 root root 16384 Mar  9 22:41 lost+found
drwxr-xr-x.   2 root root  4096 Sep 23  2011 media

```



