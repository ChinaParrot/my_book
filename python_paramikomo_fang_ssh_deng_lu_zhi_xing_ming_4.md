# python Paramiko(模仿ssh登录执行命

##安装模块


<pre>
pip install paramiko
#ubuntu 需要安装：libssl-dev 
#redhat 系列： openssl-devel
源码地址：
https://github.com/paramiko/paramiko
</pre>



## paramiko 功能

* 连接远程服务器，并执行操作

用户名和密码连接

<pre>
import paramiko
ssh.set_missing_host_key_policy(paramiko.AutoAddPolicy()) #作用是允许连接不在know_hosts文件中的主机
ssh.connect('192.168.17.248',22,'root','123456')
stdin,stdout,stderr = ssh.exec_command('df -h\nls')
ssh = paramiko.SSHClient()
print stdout.read()
#print stdin.read()
#print stderr.read()
ssh.close()
</pre>

* 上传和下载文件

<pre>
import paramiko
import os,sys
t = paramiko.Transport(('192.168.17.248',22))
t.connect(username='root',password='123456')
sftp = paramiko.SFTPClient.from_transport(t)
#上传
sftp.put('D:\log.conf','/tmp/log.conf')
#下载
sftp.get('/tmp/ks-script-mZm5Oi','D:\ks-script-mZm5Oi')
t.close()


#多文件
#!/usr/bin/env python
import paramiko
import os
import datetime
from ConfigParser import ConfigParser
ConfigFile='config.ini'
config=ConfigParser()
config.read(ConfigFile)
hostname1=''.join(config.get('IP','ipaddress'))
address=hostname1.split(';')
print address
username='root'
password='itpschina123'
port=22
local_dir='/tmp/'
remote_dir='/tmp/test/'
if __name__=="__main__":
 #    try:
        for ip in address:
                 t=paramiko.Transport((ip,port))
                 t.connect(username=username,password=password)
                 sftp=paramiko.SFTPClient.from_transport(t)
#                files=sftp.listdir(dir_path)
                 files=os.listdir(local_dir)
                 print files
                 for f in files:
                        print '####################################################'
                        print 'Begin to upload file  to %s ' % ip
                        print 'Uploading ',os.path.join(local_dir,f)

                        print datetime.datetime.now()
                        sftp.put(os.path.join(local_dir,f),os.path.join(remote_dir,f))
                        print datetime.datetime.now()
                        print '####################################################'
                 t.close()
</pre>

* 通过公私钥免密码SSH连接服务器

<pre>
#公私钥生成
ssh-keygen -t rsa
ssh-copy-id -i ~/ssh/id_rsa.pub root@192.168.17.258

import paramiko

private_key_path = '/home/auto/.ssh/id_rsa'
key = paramiko.RSAKey.from_private_key_file(private_key_path)

ssh = paramiko.SSHClient()
ssh.set_missing_host_key_policy(paramiko.AutoAddPolicy())
ssh.connect('192.168.17.258 ', 22, 'root', key)

stdin, stdout, stderr = ssh.exec_command('df')
print stdout.read()
ssh.close();

</pre>

* SSH上传和下载文件

<pre>
import paramiko

pravie_key_path = '/home/auto/.ssh/id_rsa'
key = paramiko.RSAKey.from_private_key_file(pravie_key_path)

t = paramiko.Transport(('182.92.219.86',22))
t.connect(username='wupeiqi',pkey=key)

sftp = paramiko.SFTPClient.from_transport(t)
sftp.put('/tmp/test3.py','/tmp/test3.py') 

t.close()

import paramiko

pravie_key_path = '/home/auto/.ssh/id_rsa'
key = paramiko.RSAKey.from_private_key_file(pravie_key_path)

t = paramiko.Transport(('192.168.17.258',22))
t.connect(username='root’,pkey=key)

sftp = paramiko.SFTPClient.from_transport(t)
sftp.get('/tmp/test3.py','/tmp/test4.py') 

t.close()
</pre>

* 交互式连接

<pre>
import paramiko

scp = paramiko.Transport(('192.168.2.86',22));
scp.connect(username='root',password='xxx');
channel = scp.open_session();
print channel.exec_command('mkdir hello')
channel.close();
scp.close();

import paramiko
import interactive

ssh = paramiko.SSHClient()
ssh.set_missing_host_key_policy(paramiko.AutoAddPolicy())
ssh.connect('192.168.1.108', 22, 'root', '123')

channel = ssh.invoke_shell()
interactive.interactive_shell(channel)
channel.close()
ssh.close();
</pre>