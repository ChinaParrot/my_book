# python之IP地址处理模块IPy

IP地址规划是网络设计中非常重要的一个环节，规划的好坏会直接影响路由协议算法的效率，包括网络性能、可扩展性等方面，在这个过程当中，免不了要计算大量的IP地址，包括网段、网络掩码、广播地址、子网数、IP类型等。 

```
#IPy模块包含IP类，使用它可以方便处理绝大部分格式为IPv6及IPv4的网络和地址。比如通过version方法就可以区分出IPv4与IPv6，如：
import IPy
from IPy import IP
print IP('192.168.1.0/24').version()
print IP('::1').version()

ip = IP('192.168.0.0/16')
print ip.len() #输出192.168.0.0网段的ip个数
for x in ip:
    print x

test_ip = IP('192.168.17.8')
print ip.reverseName() #反向解析地址格式
print ip.iptype() #192.168.17.8为私网类型'PRIVATE'
print IP('8.8.8.8').iptype() #8.8.8.8 为公网类型
print IP('8.8.8.8').int() #转换为整形格式
print IP('8.8.8.8').strHex() #转换为16进制
print IP('8.8.8.8').strBin() #转换为2进制
print IP(0x8080808) #16进制转换成IP格式

#IP方法也支持网络地址的转换，例如根据IP与掩码生产网段格式，如下：

from IPy import IP
print(IP('192.168.1.0').make_net('255.255.255.0'))
192.168.1.0/24
print(IP('192.168.1.0/255.255.255.0', make_net=True))
192.168.1.0/24
print(IP('192.168.1.0-192.168.1.255', make_net=True))
192.168.1.0/24

#也可以通过strNormal方法指定不同wantprefixlen参数值以定制不同输出类型的网段。输出类型为字符串，如下：
 

>>>IP('192.168.1.0/24').strNormal(0)
'192.168.1.0'
>>>IP('192.168.1.0/24').strNormal(1)
'192.168.1.0/24'
>>>IP('192.168.1.0/24').strNormal(2)
'192.168.1.0/255.255.255.0'
>>>IP('192.168.1.0/24').strNormal(3)
'192.168.1.0-192.168.1.255'

 
```

示例　根据输入的IP或子网返回网络、掩码、广播、反向解析、子网数、IP类型等信息。

```
#!/usr/bin/env python
#-*- coding:utf-8 -*-

from IPy import IP

ip_s = raw_input('请输入一个ip或 网段地址：')
ips = IP(ip_s)
if len(ips) > 1:
    print ('net: %s' % ips.net()) #输出网络地址
    print ('netmask: %s' % ips.netmask()) #输出网络地址掩码
    print ('broadcast: %s' % ips.broadcast()) #输出网络广播地址
    print ('reverse adress: %s' % ips.reverseName()[0]) #输出地址反向解析
    print ('subnet: %s' %len(ips)) #输出网络子网数
else: #为单个ip地址
    print ('reverse adress: %s' % ips.reverseName()[0])
print ('十六进制地址：%s' % ips.strHex())
print ('二进制地址：%s' % ips.strBin())
print ('IP地址类型：%s' % ips.iptype())

```

