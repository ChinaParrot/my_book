# 一、文件基本属性
Linux系统是一种典型的多用户系统，不同的用户处于不同的地位，拥有不同的权限。为了保护系统的安全性，Linux系统对不同的用户访问同一文件（包括目录文件）的权限做了不同的规定。在Linux中我们可以使用ll或者ls –l命令来显示一个文件的属性以及文件所属的用户和组，如：


```
[root@bogon ~]# ll 
-rw-r--r--. 1 root root 8835 Mar  9 22:44 install.log

```

u User，即文件或目录的拥有者；
g Group，即文件或目录的所属群组； 
o Other，除了文件或目录拥有者或所属群组之外，其他用户皆属于这个范围； a All，即全部的用户，包含拥有者，所属群组以及其他用户； 
r 读取权限，数字代号为“4”; 
w 写入权限，数字代号为“2”； 
x 执行或切换权限，数字代号为“1”； 
- 不具任何权限，数字代号为“0”； 
s 特殊功能说明：变更文件或目录的权限。


**设置权限---chmod**

chmod命令用来变更文件或目录的权限。在UNIX系统家族里，文件或目录权限的控制分别以读取、写入、执行3种一般权限来区分，另有3种特殊权限可供运用。用户可以使用chmod指令去变更文件与目录的权限，设置方式采用文字或数字代号皆可。符号连接的权限无法变更，如果用户对符号连接修改权限，其改变会作用在被连接的原始文件。

-c或——changes：效果类似“-v”参数，但仅回报更改的部分； 
-f或--quiet或——silent：不显示错误信息； 
-R或——recursive：递归处理，将指令目录下的所有文件及子目录一并处理； -v或——verbose：显示指令执行过程； 
--reference=<参考文件或目录>：把指定文件或目录的所属群组全部设成和参考文件或目录的所属群组相同； 
<权限范围>+<权限设置>：开启权限范围的文件或目录的该选项权限设置； 
<权限范围>-<权限设置>：关闭权限范围的文件或目录的该选项权限设置； 
<权限范围>=<权限设置>：指定权限范围的文件或目录的该选项权限设置；



```
1. 更改文件的属主、属组
chown：
[root@station230 ~]# chown alice.hr file1 	//改属主、属组
[root@station230 ~]# chown alice    file1 	//只改属主
[root@station230 ~]# chown      .hr file1	//只改属组
chgrp：
[root@station230 ~]# chgrp it file1		//改文件属组
[root@station230 ~]# chgrp -R it dir1		//改文件属组
	
2. 更改权限

a. 使用字符
		对象		赋值符		权限类型
		u		+		r
chmod 		g		-		w
		o		=		x
		a
[root@station230 ~]# chmod u+x file1	//属主加执行
[root@station230 ~]# chmod a=rwx file1	//所有人等于读写执行
[root@station230 ~]# chmod a=- file1	//所有人没有权限
[root@station230 ~]# chmod ug=rw,o=r file1 	 //属主属组等于读写，其他人只读
[root@station230 ~]# ll file1 			 //以长模式方式查看文件权限
-rw-rw-r-- 1 alice it 17 10-25 16:45 file1	 //显示的结果

b. 数字
[root@station230 ~]# chmod 644 file1
[root@station230 ~]# ll file1
-rw-r--r-- 1 alice it 17 10-25 16:45 file1
```


