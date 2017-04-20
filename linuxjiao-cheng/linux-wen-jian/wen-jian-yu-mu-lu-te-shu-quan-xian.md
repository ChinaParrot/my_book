# Linux下的文件权限

在linux下每一个文件和目录都有自己的访问权限，访问权限确定了用户能否访问文件或者目录和怎样进行访问。最为我们熟知的一个文件或目录可能拥有三种权限，分别是读、写、和执行操作，在这里不做详细说明。我们创建一个文件后系统会默认地赋予所有者读和写权限。当然我们也可以自己修改它，添加自己需要的权限。

# 特殊权限

## suid	(4)

1)SUID只能用于二进制可执行文件，对目录无效
2)执行者若具有该文件的x权限，则将具有文件所有者的权限
3)权限只在文件执行时有效，执行完毕不再拥有所有者权限

当文件被设定setuid位以后，任何可以运行此文件的用户都可以像文件属主一样运行它，听着别扭，举个例子：如果你给/bin/rm设置setuid权限位，也即将原来的“-rwxr-xr-x”改成了“-rwsr-xr-x”，那么所有用户都可以利用这个rm程序来删掉系统内的任何文件。当文件本来就没有可执行权限还加上setuid属性时，权限位就用“S”表示，像这样“-rwSr–r–”。 

## sgid (2)	

SGID和SUID不同，可以用于目录
1)使用者若有此目录的x,w权限，则可进入和修改此目录
2)使用者在此目录下的群组将变成该目录的群组，新建的文件，群组是此目录的群组。

与setuid功能类似，setgid权限位被设定以后，任何用户都拥有了该文件所属组的权限，也就是可以像该文件组内成员一样运行它。另外当一个目录被设置setgid位后，以后复制到这个目录下的文件的组权限自动被改成目录文件所在组，除非复制是加上-p (preserve)选项。

## sticky bit（粘滞位|1）

1)和SUID,SGID不同的是，只能用于目录
2)使用者在该目录下，仅自己与root才有权力删除新建的目录或文件

当sticky位被设置以后，只有root或者文件所有这才能删除或移动它，例如/tmp目录就被设了sticky位“drwxrwxrwt”，这样所有的用户都对这个文件夹可读可写，却只有root（/tmp属主）能删除或移动它。 


**授权使用**


```
chmod u+s xxx # 设置setuid权限

chmod g+s xxx # 设置setgid权限

chmod o+t xxx # 设置stick bit权限，针对目录

chmod 4775 xxx # 设置setuid权限

chmod 2775 xxx # 设置setgid权限

chmod 1775 xxx # 设置stick bit权限，针对目录
```

# ACL权限规划

ACL 是 Access Control List 的缩写，主要的目的是在提供传统的 owner,group,others 的 read,write,execute 权限之外的细部权限配置。ACL 可以针对单一使用者，单一文件或目录来进行 r,w,x 的权限规范，对于需要特殊权限的使用状况非常有帮助。

那 ACL 主要可以针对哪些方面来控制权限呢？他主要可以针对几个项目：

使用者 (user)：可以针对使用者来配置权限；
群组 (group)：针对群组为对象来配置其权限；
默认属性 (mask)：还可以针对在该目录下在创建新文件/目录时，规范新数据的默认权限；
## 1、查看是否支持acl

由于 ACL 是传统的 Unix-like 操作系统权限的额外支持项目，因此要使用 ACL 必须要有文件系统的支持才行。目前绝大部分的文件系统都有支持 ACL 的功能，包括 ReiserFS, EXT2/EXT3, JFS, XFS 等等。在我们的 CentOS 6.x 当中，默认使用 Ext4 是启动 ACL 支持的！至于察看你的文件系统是否支持 ACL 可以这样看：
```
[root@bogon /]# mount
/dev/sda3 on / type ext4 (rw)
proc on /proc type proc (rw)
sysfs on /sys type sysfs (rw)
devpts on /dev/pts type devpts (rw,gid=5,mode=620)
tmpfs on /dev/shm type tmpfs (rw)
/dev/sda1 on /boot type ext4 (rw)
none on /proc/sys/fs/binfmt_misc type binfmt_misc (rw)

[root@bogon /]# dumpe2fs  -h /dev/sda3 |grep acl
dumpe2fs 1.41.12 (17-May-2010)
Default mount options:    user_xattr acl

```

## 2、setfacl 命令用法



```
[root@www ~]# setfacl [-bkRd] [{-m|-x} acl参数] 目标文件名
选项与参数：
-m ：配置后续的 acl 参数给文件使用，不可与 -x 合用；
-x ：删除后续的 acl 参数，不可与 -m 合用；
-b ：移除所有的 ACL 配置参数；
-k ：移除默认的 ACL 参数，关于所谓的『默认』参数于后续范例中介绍；
-R ：递归配置 acl ，亦即包括次目录都会被配置起来；
-d ：配置『默认 acl 参数』的意思！只对目录有效，在该目录新建的数据会引用此默认值

# 1. 针对特定使用者的方式：
# 配置规范：『 u:[使用者账号列表]:[rwx] 』，例如针对 vbird1 的权限规范 rx ：
[root@www ~]# touch acl_test1
[root@www ~]# ll acl_test1
-rw-r--r-- 1 root root 0 Feb 27 13:28 acl_test1
[root@www ~]# setfacl -m u:vbird1:rx acl_test1
[root@www ~]# ll acl_test1
-rw-r-xr--+ 1 root root 0 Feb 27 13:28 acl_test1
# 权限部分多了个 + ，且与原本的权限 (644) 看起来差异很大！但要如何查阅呢？

[root@www ~]# setfacl -m u::rwx acl_test1
[root@www ~]# ll acl_test1
-rwxr-xr--+ 1 root root 0 Feb 27 13:28 acl_test1
# 无使用者列表，代表配置该文件拥有者，所以上面显示 root 的权限成为 rwx 了！
```



## 3、 
