# 1、shell
Shell 是一个用C语言编写的程序，它是用户使用Linux的桥梁。Shell既是一种命令语言，又是一种程序设计语言。Shell 是指一种应用程序，这个应用程序提供了一个界面，用户通过这个界面访问操作系统内核的服务。Ken Thompson的sh是第一种Unix Shell，Windows Explorer是一个典型的图形界面Shell。常用的shell是Bourne Again Shell（/bin/bash）。

# 2 、简单shell


```
#!/bin/bash
. /etc/profile #加载用户环境变量
date
who
# test    # “#” shell 注释
```

# 3 、 命令手册

```
yum -y install man

man [命令名称]
```

看不懂英文只好找百度。

#4、 了解 linux 基础

 * ** 查看文件时间**



ls -l 文件名 	仅看的是文件的修改时间

Linux文件有三种时间：stat 例如：stat profile.d/

访问时间：atime，查看 内容

修改时间：mtime，修改 内容

改变时间：ctime，文件 属性，比如权限

```
[root@bogon ~]# ls -l install.log
-rw-r--r--. 1 root root 8835 Mar  9 22:44 install.log
[root@bogon ~]# stat install.log
  File: `install.log'
  Size: 8835      	Blocks: 24         IO Block: 4096   regular file
Device: 803h/2051d	Inode: 261123      Links: 1
Access: (0644/-rw-r--r--)  Uid: (    0/    root)   Gid: (    0/    root)
Access: 2017-03-09 22:41:58.253999993 +0800
Modify: 2017-03-09 22:44:28.421999932 +0800
Change: 2017-03-09 22:44:31.710999932 +0800

```

* **文件类型**


