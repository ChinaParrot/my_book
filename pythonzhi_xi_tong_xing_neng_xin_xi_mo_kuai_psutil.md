# python之系统性能信息模块psutil


psutil是一个跨平台库，能够轻松的实现获取系统运行的进程和系统利用率（包括CPU、内存、磁盘、网络等）信息。它主要应用于系统监控，分析和限制系统资源及进程的管理。它实现了同等命令行工具提供的功能，如ps、top、lsof、netstat、ifconfig、who、df、kill、free、nice、ionice、iostat、iotop、uptime、pidof、tty、taskset、pmap等。目前支持32位和64位的Linux、Windows、OS X、FreeBSD和Sun Solaris等操作系统，支持从2.4到3.4的Python版本，目前最新版本为4.3.0。



#实例详解

```
#!/usr/bin/env python
#-*- coding:utf-8 -*-

import psutil

'''
安装pip install psutil

或者
#install psutil
https://code.google.com/archive/p/psutil/

下载地址：https://github.com/giampaolo/psutil
https://pypi.python.org/packages/source/p/psutil/psutil-4.3.0.tar.gz

tar xvf psutil-4.3.0.tar.gz
python setup.py install

'''

#psutil 库采用的是字节
'''
8bit(位)=1Byte(字节)
1024Byte(字节)=1KB
1024KB=1MB
1024MB=1GB
1024GB=1TB
'''

#（01）获取cpu信息
#显示所有逻辑CPU信息。
print psutil.cpu_times(percpu=True)
#获取CPU的逻辑个数
print psutil.cpu_count()
#获取物理cpu个数
print psutil.cpu_count(logical=False)


#（02）内存信息
print psutil.virtual_memory()
#获取内存总数
print psutil.virtual_memory().total
#获取空闲内存数
print psutil.virtual_memory().free
#获取swap信息
print psutil.swap_memory()


#（03）磁盘信息
print psutil.disk_partitions(all=True)
#获取分区参数
print psutil.disk_usage('d:\\')
#获取磁盘IO个数
print psutil.disk_io_counters()


#（04）网络信息
#获取网络总的IO信息
print psutil.net_io_counters()
#获取每个网络接口的io信息
print psutil.net_io_counters(pernic=True)


#其他信息
#返回当前用户登录信息
print psutil.users()
#获取开机时间（以时间戳的方式）
print psutil.boot_time()
import datetime
print datetime.datetime.fromtimestamp(psutil.boot_time()).strftime("%Y-%m-%d %H:%M:%S")


##系统进程管理方法
#（1）进程信息

print psutil.pids() #获取所有进程的PID

p = psutil.Process(2128) #实例化一个Process对象，参数为一个进程PID
print p.name() #进程名
print p.exe() #经常bin路径
print p.cwd() #进程工作目录路径
print p.status() #进程状态
print p.create_time() #进程创建时间，时间戳格式
print p.uids() #进程uid信息
print p.gids() #进程gid信息
print p.cpu_times() #进程cpu时间信息，包括use,system两个时间
print p.cpu_affinity() #get进程CPU亲合度，如果设置了进程cpu的亲和度，降CPU号作为参数即可
print p.memory_percent() #进程内存利用率
print p.memory_info() #进程内存rss.vms信息
print p.io_counters() #进程IO信息，包括读写IO数及字节数
print p.connections() #返回打开进程socket的namedutples列表，包括fs、family、laddr等信息
print p.num_threads() #进程开启的线程数


##popen类的使用
from subprocess import PIPE
#通过psutil的popen方法启动的应用程序，可以跟踪程序运行的所有相关信息
p = psutil.Popen(['/usr/bin/python','-c','print ("hello")'],stdout=PIPE)
print p.name()
print p.username()
print p.communicate()
print p.cpu_times()



```

