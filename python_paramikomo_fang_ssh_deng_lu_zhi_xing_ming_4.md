用户名和密码连接

# python Paramiko(模仿ssh登录执行命

##安装模块

```pip install paramiko```


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
