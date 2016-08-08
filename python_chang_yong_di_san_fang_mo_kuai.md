# Python常用第三方、内置模块

scapy（http://www.secdev.org/projects/scapy/） 是一个强大的交互式数据包处理程序，它能够对数据包进行伪造或解包，包括发送数据包、包嗅探、应答和反馈匹配等功能。可以用在处理网络扫描、路由跟踪、服务探测、单元测试等方面，本节主要针对scapy的路由跟踪功能，实现TCP协议方式对服务可用性的探测，比如常用的80（HTTP）与443（HTTPS）服务，并生成美观的路由线路图报表，让管理员清晰了解探测点到目标主机的服务状态、骨干路由节点所处的IDC位置、经过的运营商路由节点等信息

安装：

```
# scapy模板需要tcpdump程序支持，生成报表需要graphviz、ImageMagick图像处理包支持  
# yum -y install tcpdump graphviz ImageMagick  
 
# 源码安装  
# wget http://www.secdev.org/projects/scapy/files/scapy-2.2.0.tar.gz  
# tar -zxvf scapy-2.2.0.tar.gz  
# cd scapy-2.2.0  
# python setup.py install 
```

scapy模块提供了众多网络数据包操作的方法，包括发包send()、SYN\ ACK扫描、嗅探sniff()、抓包wrpcap()、TCP路由跟踪traceroute()等，本节主要关注服务监控内容接下来详细介绍traceroute()方法，其具体定义如下：
 

```
traceroute(target, dport=80, minttl=1, maxttl=30, sport=<RandShort>, l4=None, filter=None, timeout=2, verbose=None, **kargs) 
```

该方法实现TCP跟踪路由功能，关键参数说明如下：

* target：跟踪的目标对象，可以是域名或IP，类型为列表，支持同时指定多个目标，如["www.qq.com","www.baidu.com","www.google.com.hk"]；

* dport：目标端口，类型为列表，支持同时指定多个端口，如[80,443]；

* minttl：指定路由跟踪的最小跳数（节点数）；

* maxttl：指定路由跟踪的最大跳数（节点数）。
 
 
实现TCP探测目标服务路由轨迹

```
#!/usr/bin/env python
#-*- coding:utf-8 -*-

import os,sys,time,subprocess  
import warnings,logging  
warnings.filterwarnings("ignore", category=DeprecationWarning) #屏蔽scapy无用告警信息  
logging.getLogger("scapy.runtime").setLevel(logging.ERROR) #屏蔽模块IPv6多余告警  
from scapy.all import traceroute  
 
domains = raw_input('Please input one or more IP/domain: ') #接受输入的域名或IP  
target =  domains.split(' ')  
dport = [80]    #扫描的端口列表  
 
if len(target) >= 1 and target[0]!='':  
    res,unans = traceroute(target,dport=dport,retry=-2) #启动路由跟踪  
    res.graph(target="> test.svg")    #生成svg矢量图形  
    time.sleep(1)  
    subprocess.Popen("/usr/bin/convert test.svg test.png", shell=True) #svg转png格式  
else:  
    print "IP/domain number of errors,exit" 
```
