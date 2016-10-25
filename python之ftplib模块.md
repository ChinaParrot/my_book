# Python 之ftplib模块

python中默认安装的ftplib模块定义了FTP类，其中函数有限，可用来实现简单的ftp客户端，用于上传或下载文件，函数列举如下

 相关方法：

```
ftp.cwd(pathname) #设置FTP当前操作的路径

ftp.dir() #显示目录下所有目录信息

ftp.nlst() #获取目录下的文件

ftp.mkd(pathname) #新建远程目录

ftp.pwd() #返回当前所在位置

ftp.rmd(dirname) #删除远程目录

ftp.delete(filename) #删除远程文件

ftp.rename(fromname, toname)#将fromname修改名称为toname。

ftp.storbinaly("STOR filename.txt",file_handel,bufsize) #上传目标文件

ftp.retrbinary("RETR filename.txt",file_handel,bufsize) #下载FTP文件
```


