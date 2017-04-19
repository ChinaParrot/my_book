# 1、shell
Shell 是一个用C语言编写的程序，它是用户使用Linux的桥梁。Shell既是一种命令语言，又是一种程序设计语言。Shell 是指一种应用程序，这个应用程序提供了一个界面，用户通过这个界面访问操作系统内核的服务。Ken Thompson的sh是第一种Unix Shell，Windows Explorer是一个典型的图形界面Shell。常用的shell是Bourne Again Shell（/bin/bash）。

**bash功能**
 *  命令和文件自动补全<tab>  注意：Tab只能补全命令和文件
 *  快捷键



```
^c   终止前台运行的程序 或者 另起一行
^d   结束
^l   清屏 
^a   光标到命令行的最前端
^e   。。。。。。。。后端
^r   搜索历史命令，利用关键词

```
* 历史命令




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

通过颜色判断文件的类型是完全错误的！！！

Linux文件是没有扩展名！！！

方法一：

ls -l  文件名    //看第一个字符

\-	普通文件（文本文件，二进制，电影，图片。。。）
d	目录文件（蓝色）
b	设备文件（块设备）存储设备硬盘，U盘
c	设备文件（字符设备）打印机，终端
s	套接字文件
p	管道文件
l	链接文件（淡蓝色）

方法二：file

file /bin/ls
file /home
file /dev/sda


