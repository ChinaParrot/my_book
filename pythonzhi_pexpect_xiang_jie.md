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
参数timeout为等待结果的超时时间；参数maxread 为pexpect从终端控制台一次读取的最大字节数，searchwindowsize 参数为匹配缓冲区字符串的位置，默认是从开始位置匹配。

注意的是，pexpect不会解析shell命令中的元字符，包括重定向‘>’、管道‘|’或者‘*’，当然我没有可以通过将这三个特殊元字符的命令作为/bin/bash 的参数进行调用，例如

```
child = pexpect.spawn('/bin/bash -c "ls -l|grep LOG >logs.txt"')
child.expect(pexpect.EOF)

```
或者

```
shell_cmd = 'ls -l |grep LOG>logs.txt'
child = pexpect.spawn('/bin/bash',['-c',shell_cmd]
child.expect(pexpect.EOF)
```

pexpect提供了2种途径写入log，一种为写到日志文件，另一种是标准输出。

```
写入日志文件：
child = pexpect.spawn('some_command')
fout = file('mylog.txt','w')
child.logfile = fout

输出控制台：
child = pexpect.spawn('some_command')
child.logfile = sys.stdout
```

* expect方法

expect定义了一个子程序输出的匹配规则。
方法定义： expect(pattern,timeout=30,searchwindowsize=None)
其中，参数pattern表示字符串、pexpect.EOF(指向缓冲区尾部，无匹配项)、pexpect.TIMEOUT(匹配等待超时）、正则表达式或者前面四种类型组成的列表（List），当pattern为一个列表时，且不止一个表列元素被匹配，则返回的结果是子程序输出最先出现的那个元素，或者是列表最左边的元素（最小索引ID）

```
import pexpect
child = pexpect.spawn("echo 'foobar'")
print child.expect(['bar','foo','foobar'])
输出：1，即'foo'被匹配
```
参数timeout 指定等待匹配结果的超时时间，单位为秒。当超时被触发时，expect将匹配到pexpect.TIMEOUT;参数searchwindows为匹配缓冲区字符串的位置，默认是从开始位置匹配。

当pexpect.EOF、pexpect.TIMEOUT作为列表参数时，匹配时将返回处列表中的索引ID,例如：

```
index = p.expect(['good','bad',pexpect.EOF,pexpect.TIMEOUT])
if index == 0:
  do_someting()
elif index ==1:
  do_something_else()
elif index ==2:
  do_some_other_thing()
elif index ==3:
  do_something_completely_different()
  
```
以上等价于

```
try: 
  index = p.expect(['good','bad'])
  if index == 0:
    do_something()
  elif index == 1:
    do_something_else()
  except EOF:
    do_some_other_thiing()
  except TIMEOUT:
    do_something_completely_different()
    
```
expect 方法有两个非常棒的成员：before与after。before成员保存了最近匹配成功之前的内容，after成员保存了最近匹配成功之后的内容。例如：

```
import pexpect
import sys
child = pexpect.spawn('ssh  root@127.0.0.1')
fout = file('mylog.txt','w')
#child.logfile = fout
child.logfile = sys.stdout
child.expect('password:')
child.sendline('123456')
print "before:" + child.before
print "after:" + child.after

运行结果：

before： root@127.0.0.1's
agter: password:
```
 * read 相关方法

下面这些输入方法的作用都是向子程序发送响应命令，可以理解成代替了我们的标准输入键盘。

```
send(self,s) 发送命令，不回车
sendline(self,s='')发送命令，回车
sendcontrol(self,char) 发送控制字符，如child.sendcontrol('c') 等价于"Ctrl+c"

sendeof() 发送eof

```

实例：ssh 的使用
```
#!/usr/bin/env python

"""
This runs a command on a remote host using SSH. At the prompts enter hostname,
user, password and the command.
"""

import pexpect
import getpass, os

#user: ssh 主机的用户名
#host：ssh 主机的域名
#password：ssh 主机的密码
#command：即将在远端 ssh 主机上运行的命令
def ssh_command (user, host, password, command):
    """
    This runs a command on the remote host. This could also be done with the
    pxssh class, but this demonstrates what that class does at a simpler level.
    This returns a pexpect.spawn object. This handles the case when you try to
    connect to a new host and ssh asks you if you want to accept the public key
    fingerprint and continue connecting.
    """
    ssh_newkey = 'Are you sure you want to continue connecting'
    # 为 ssh 命令生成一个 spawn 类的子程序对象.
    child = pexpect.spawn('ssh -l %s %s %s'%(user, host, command))
    i = child.expect([pexpect.TIMEOUT, ssh_newkey, 'password: '])
    # 如果登录超时，打印出错信息，并退出.
    if i == 0: # Timeout
        print 'ERROR!'
        print 'SSH could not login. Here is what SSH said:'
        print child.before, child.after
        return None
    # 如果 ssh 没有 public key，接受它.
    if i == 1: # SSH does not have the public key. Just accept it.
        child.sendline ('yes')
        child.expect ('password: ')
        i = child.expect([pexpect.TIMEOUT, 'password: '])
        if i == 0: # Timeout
        print 'ERROR!'
        print 'SSH could not login. Here is what SSH said:'
        print child.before, child.after
        return None
    # 输入密码.
    child.sendline(password)
    return child

def main ():
    # 获得用户指定 ssh 主机域名.
    host = raw_input('Hostname: ')
    # 获得用户指定 ssh 主机用户名.
    user = raw_input('User: ')
    # 获得用户指定 ssh 主机密码.
    password = getpass.getpass()
    # 获得用户指定 ssh 主机上即将运行的命令.
    command = raw_input('Enter the command: ')
    child = ssh_command (user, host, password, command)
    # 匹配 pexpect.EOF
    child.expect(pexpect.EOF)
    # 输出命令结果.
    print child.before

if __name__ == '__main__':
    try:
        main()
    except Exception, e:
        print str(e)
        traceback.print_exc()
        os._exit(1)
```

 
 ##run函数
  run是使用pexpect进行封装的调用外部命令的函数，类似os.system或os.popen方法，不同的是，使用run()可以同时获得命令的输出结果及命令的退出状态。
  
  ```
  run(command, timeout=-1, withexitstatus=False, events=None, extra_args=None, logfile=None, cwd=None, env=None)
#默认情况下该指令：
#1.运行给出的指令command，如果指令不是以绝对路径给出，会自动在PATH中寻找。结果输出作为字符串返回，行与行之间以\r\n分割。
#2.withexitstatus设置为True时，结果返回一个元组，(command_output,
    exitstatus)
#events是一个字典，有模式和应答组成，可以自动输入内容，如果应答需要输入enter键时，此时需要为一个新行，即添加\n.
>>> pexpect.run('cat /root/a.txt')
'qian shan\r\nniao fei jue\r\ndu diao han jiang xue\r\n'
>>> pexpect.run('cat /root/a.txt',withexitstatus=1)
('qian shan\r\nniao fei jue\r\ndu diao han jiang xue\r\n', 0)
>>> pexpect.run('scp /root/a.txt 192.168.56.102:/root',withexitstatus=1,events={'password': '123456\n'})
("root@192.168.56.102's password: \r\n\ra.txt        
  ```
  ##pxssh 类
  
  pxssh 是pexpect的派生类，针对上ssh会话操作上再做一层封装，提供与基类更加直接的操作方法。
  pxssh 类定义：
  ```
  class pexpect.pxssh.pxssh(timeout=30,maxread=2000,searchwindow=None,logfile=None,cwd=None,env=None)
  
  ```
  
  * login() 建立ssh连接；
  * logout()断开连接；
  * prompt()等待系统提示符，用于等待命令执行结束。
  
  例子：
  
  
  ```
  
 #!/usr/bin/env python
 #-*- coding:utf-8 -*-

import pxssh
import getpass
try:
    # 调用构造函数，创建一个 pxssh 类的对象.
    s = pxssh.pxssh()
    # 获得用户指定 ssh 主机域名.
    hostname = raw_input('hostname: ')
    # 获得用户指定 ssh 主机用户名.
    username = raw_input('username: ')
    # 获得用户指定 ssh 主机密码.
    password = getpass.getpass('password: ')
    #ssh 端口
    port = raw_input('port:')
    # 利用 pxssh 类的 login 方法进行 ssh 登录，原始 prompt 为'$' , '#'或'>'
    s.login (hostname, username, password, port=port ,original_prompt='[$#>]')

    # 发送命令 'uptime'
    s.sendline ('uptime')
    # 匹配 prompt
    s.prompt()
    # 将 prompt 前所有内容打印出，即命令 'uptime' 的执行结果.
    print s.before
    # 发送命令 ' ls -l '
    s.sendline ('ls -l')
    # 匹配 prompt
    s.prompt()
    # 将 prompt 前所有内容打印出，即命令 ' ls -l ' 的执行结果.
    print s.before
    # 退出 ssh session
    s.logout()
except pxssh.ExceptionPxssh, e:
    print "pxssh failed on login."
    print str(e) 
    
  ```
  
  实现自动化ftp操作
  
  ```
  #!/usr/bin/env python
#-*- coding:utf-8 -*-

from __future__ import unicode_literals #使用Unicode编码
import pexpect
import sys

child = pexpect.spawnu('ftp www.jqlinux.com') #运行ftp命令
child.expect('(?i)name .*:') #(?i)表示后面的字符串正则匹配忽略大小写
child.sendline('root') #输入ftp账号信息
child.expect('(?i)password') #匹配密码输入提示
child.sendline('123456')
child.expect('ftp>')
child.sendline('get python_test/scapy-test.py') #下载文件
child.expect('ftp>')
sys.stdout.write(child.before) #输出匹配“ftp>” 之前的输入与输出
print("Escape character is '^]'.\n")
sys.stdout.write(child.after)
sys.stdout.flush()
#调用interract()让出控制权，用户可以继续当前的回话手工控制程序，默认输入“^]” 字符跳出child.interact()
child.sendline('bye')
child.close()
  ```
  
  