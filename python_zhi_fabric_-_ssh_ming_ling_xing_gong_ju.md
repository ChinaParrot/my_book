 # python 之Fabric-SSH命令行工具


Fabric是基于python2.5及以上版本实现的SSH命令行工具，简化了SSH应用程序部署及系统管理任务，他提供了系统基础的操作组件，可以实现本地或远程shell命令，包括命令执行、文件上传、下载及完整执行日志输出等功能。Fabric在paramiko的基础上做更高一层的封装，操作起来更加简单。

官网地址：http://www.fabfile.org/

##fab的常用参数
``````
Usage: fab [options] <command>[:arg1,arg2=val2,host=foo,hosts='h1;h2',...] ...

```

* -l,显示定义好的任务函数名；
* -f,指定fab入口文件，默认入口文件名为fabfile.py
* -g,指定网关（中转）设备，比如堡垒机环境，填写堡垒机ip即可
* -H,指定目标主机，多台主机用“，”号分隔；
* -P,以异步并行方式运行多主机任务，默认为串行运行；
* -R,指定role，以角色名区分不同业务组设备；
* -t，设置设备连接超时时间（秒）；
* -T,设置远程主机命令执行超时时间（秒）；
* -w,当命令执行失败，发出告警，而非默认终止任务。

有时候我们可已不需要写一行python代码也可以完成远程操作，直接使用命令的形式，例如：

```
fab -p 123456(密码) -H 192.168.1.21,192.168.1.22 -- 'uname -s'

```

##fabric的环境变量

fabric的环境变量有很多，存放在一个字典中，
fabric.state.env，而它包含在fabric.api中。
为了方便，我们一般使用env来指代环境变量。
env环境变量可以控制很多fabric的行为，一般通过env.xxx可以进行设置。
 
fabric默认使用本地用户通过ssh进行连接远程机器，不过你可以通过env.user变量进行覆盖。
当你进行ssh连接时，fabric会让你交互的让你输入远程机器密码，如果你设置了env.password变量，则就不需要交互的输入密码。
下面介绍一些常用的环境变量：

* abort_on_prompts    设置是否运行在交互模式下，例如会提示输入密码之类，默认是false
* connection_attempts    fabric尝试连接到新服务器的次数，默认1次
* cwd    目前的工作目录，一般用来确定cd命令的上下文环境
* disable_known_hosts    默认是false，如果是true，则会跳过用户知道的hosts文件
* exclude_hosts    指定一个主机列表，在fab执行时，忽略列表中的机器
* fabfile    默认值是fabfile.py在fab命令执行时，会自动搜索这个文件执行。
* host_string    当fabric连接远程机器执行run、put时，设置的user/host/port等
* hosts    一个全局的host列表
* keepalive    默认0 设置ssh的keepalive
* loacl_user    一个只读的变量，包含了本地的系统用户，同user变量一样，但是user可以修改
* parallel    默认false，如果是true则会并行的执行所有的task
* pool_size    默认0 在使用parallel执行任务时设置的进程数
* password    ssh远程连接时使用的密码，也可以是在使用sudo时使用的密码
* passwords    一个字典，可以为每一台机器设置一个密码，key是ip，value是密码
* path    在使用run/sudo/local执行命令时设置的$PATH环境变量
* port    设置主机的端口
* roledefs    一个字典，设置主机名到规则组的映射
* roles    一个全局的role列表
* shell    默认是/bin/bash -1 -c 在执行run命令时，默认的shell环境
* skip_bad_hosts    默认false，为ture时，会导致fab跳过无法连接的主机
* sudo_prefix    默认值"sudo -S -p '%(sudo_prompt)s' " % env 执行sudo命令时调用的sudo环境
* sudo_prompt    默认值"sudo password:"
* timeout    默认10 网络连接的超时时间
* user   ssh使用哪个用户登录远程主机
* local  执行本地命令，如： local('uname -s')
* lcd   切换本地目录，如： lcd('/home')
* cd 切换远程目录，如： cd('/data/logs')
* run 执行远程命令 如： run('free -m')
* sudo sudo方式执行命令，如sudo('/etc/init.d/httpd start')
* put 上传
