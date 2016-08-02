# Python之DNS处理模块dnspython

dnspython（http://www.dnspython.org/） 是Python实现的一个DNS工具包，它支持几乎所有的记录类型，可以用于查询、传输并动态更新ZONE信息，同时支持TSIG（事务签名）验证消息和EDNS0（扩展DNS）。在系统管理方面，我们可以利用其查询功能来实现DNS服务监控以及解析结果的校验，可以代替nslookup及dig等工具，轻松做到与现有平台的整合。

dnspython模块提供了大量的DNS处理方法，最常用的方法是域名查询。dnspython提供了一个DNS解析器类—resolver，使用它的query方法来实现域名的查询功能。query方法的定义如下：
 
```
query(self, qname, rdtype=1, rdclass=1, tcp=False, source=None, raise_on_no_answer=True, source_port=0) 

```

其中，qname参数为查询的域名。rdtype参数用来指定RR资源的类型，常用的有以下几种：

A记录，将主机名转换成IP地址；

MX记录，邮件交换记录，定义邮件服务器的域名；

CNAME记录，指别名记录，实现域名间的映射；

NS记录，标记区域的域名服务器及授权子域；

PTR记录，反向解析，与A记录相反，将IP转换成主机名；

SOA记录，SOA标记，一个起始授权区的定义。

rdclass参数用于指定网络类型，可选的值有IN、CH与HS，其中IN为默认，使用最广泛。tcp参数用于指定查询是否启用TCP协议，默认为False（不启用）。source与source_port参数作为指定查询源地址与端口，默认值为查询设备IP地址和0。raise_on_no_answer参数用于指定当查询无应答时是否触发异常，默认为True。

实例：

* A记录查询

```
#!/usr/bin/env python
#-*- coding:utf-8 -*-

import dns.resolver

def main():
    var = 1
    while var == 1:
        domain = raw_input('Please input an domain: ')    #输入域名地址
        A = dns.resolver.query(domain, 'A')    #指定查询类型为A记录
        for i in A.response.answer:   #通过response.answer方法获取查询回应信息
            for j in i.items:
                print j.address

if __name__ == '__main__':
    main()
```

* max记录查询

```
#!/usr/bin/env python
#-*- coding:utf-8 -*-

import dns.resolver
domain = raw_input("Please input an domain:")
MX = dns.resolver.query(domain,'MX')#指定查询记录类型为max
for i in MX:
    print'MX preference=',i.preference,' mail exchanger=',i.exchange

```




