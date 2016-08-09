# python之pexpect详解

pexpect 是linux下expect的python封装，通过pexpect我们可以实现对ssh、ftp、password、telnet等命令进行自动交互，无需人工达到自动化需求。

下载安装：
http://pexpect.readthedocs.io/en/stable/install.html

```
import pexpect
child = pexpect.spawn('scp foo user@example.com:.') #spawn 启动scp程序
child.expect('Password:') #expect方法等待子程序产生的输出，判断是否匹配定义的字符串 'Password:'
child.sendline(mypassword) #匹配后则发送密码串进行回应

```

##spawn 类

spawn是pexpect的主要类接口，功能是启动和控制子应用程序。

```
class pexpect.spawn(command,args=[],timeout=30,maxread=2000,searchwindowsize=None,logfile=None,cwd=None,env=None,ignore_sighup=True)

```
其中command参数可以是任意已知的系统命令，比如：

```
child = pexpect.spawn('/usr/bin/ftp') 
child = pexpect.spawn('/usr/bin/ssh user@example.com')
child = pexpect.spawn('ls -latr /tmp') 
```
当子程序需要参数时，还可以使用python列表来代替参数项：

```
child = pexpect.spawn('/usr/bin/ftp',[]) 
child = pexpect.spawn('/usr/bin/ssh' ,['user@example.com'])
child = pexpect.spawn('ls', ['-latr', '/tmp']) 
```
