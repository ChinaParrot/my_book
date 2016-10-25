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

ftp登陆连接


```

 print "LocalDir:", LocalDir

 return



 def DownLoadFileTree(self, LocalDir, RemoteDir):

 print "remoteDir:", RemoteDir

 if os.path.isdir( LocalDir ) == False:

 os.makedirs( LocalDir )

 self.ftp.cwd( RemoteDir )

 RemoteNames = self.ftp.nlst()

 print "RemoteNames", RemoteNames

 print self.ftp.nlst("/del1")

 for file in RemoteNames:

 Local = os.path.join( LocalDir, file )

 if self.isDir( file ):

 self.DownLoadFileTree( Local, file )

 else:

 self.DownLoadFile( Local, file )

 self.ftp.cwd( ".." )

 return



 def show(self, list):

 result = list.lower().split( " " )

 if self.path in result and "<dir>" in result:

 self.bIsDir = True



 def isDir(self, path):

 self.bIsDir = False

 self.path = path

 #this ues callback function ,that will change bIsDir value

 self.ftp.retrlines( 'LIST', self.show )

 return self.bIsDir



 def close(self):

 self.ftp.quit()

if __name__ == "__main__":

 ftp = myFtp('*****')

 ftp.Login('***','***')

 ftp.DownLoadFileTree('del', '/del1')#ok

 ftp.UpLoadFileTree('del', "/del1" )

 ftp.close()

 print "ok!"


```