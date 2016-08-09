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

##expect方法

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
