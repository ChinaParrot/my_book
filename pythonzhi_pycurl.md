# Python之pycurl
下面介绍Curl对象几个常用的方法。

<pre> 
close()方法，对应libcurl包中的curl_easy_cleanup方法，无参数，实现关闭、回收Curl对象。
 
perform()方法，对应libcurl包中的curl_easy_perform方法，无参数，实现Curl对象请求的提交。
 
setopt(option, value)方法，对应libcurl包中的curl_easy_setopt方法，参数option是通过libcurl的常量来指定的，参数value的值会依赖option，可以是一个字符串、整型、长整型、文件对象、列表或函数等。
  
下面列举常用的常量列表：
 
c = pycurl.Curl()    #创建一个curl对象
c.setopt(pycurl.CONNECTTIMEOUT, 5)    #连接的等待时间，设置为0则不等待
c.setopt(pycurl.TIMEOUT, 5)    #请求超时时间
c.setopt(pycurl.NOPROGRESS, 0)    #是否屏蔽下载进度条，非0则屏蔽
c.setopt(pycurl.MAXREDIRS, 5)    #指定HTTP重定向的最大数
c.setopt(pycurl.FORBID_REUSE, 1)    #完成交互后强制断开连接，不重用
c.setopt(pycurl.FRESH_CONNECT,1)    #强制获取新的连接，即替代缓存中的连接
c.setopt(pycurl.DNS_CACHE_TIMEOUT,60)    #设置保存DNS信息的时间，默认为120秒
c.setopt(pycurl.URL,"http://www.baidu.com")    #指定请求的URL
c.setopt(pycurl.USERAGENT,"Mozilla/5.2 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322; .NET CLR 2.0.50324)")    #配置请求HTTP头的User-Agent
c.setopt(pycurl.HEADERFUNCTION, getheader)  #将返回的HTTP HEADER定向到回调函数getheader
c.setopt(pycurl.WRITEFUNCTION, getbody)    #将返回的内容定向到回调函数getbody
c.setopt(pycurl.WRITEHEADER, fileobj)     #将返回的HTTP HEADER定向到fileobj文件对象
c.setopt(pycurl.WRITEDATA, fileobj)    #将返回的HTML内容定向到fileobj文件对象
getinfo(option)方法，对应libcurl包中的curl_easy_getinfo方法，参数option是通过libcurl的常量来指定的。

下面列举常用的常量列表：
c = pycurl.Curl()    #创建一个curl对象
c.getinfo(pycurl.HTTP_CODE)    #返回的HTTP状态码
c.getinfo(pycurl.TOTAL_TIME)    #传输结束所消耗的总时间
c.getinfo(pycurl.NAMELOOKUP_TIME)    #DNS解析所消耗的时间
c.getinfo(pycurl.CONNECT_TIME)    #建立连接所消耗的时间
c.getinfo(pycurl.PRETRANSFER_TIME)    #从建立连接到准备传输所消耗的时间
c.getinfo(pycurl.STARTTRANSFER_TIME)    #从建立连接到传输开始消耗的时间
c.getinfo(pycurl.REDIRECT_TIME)    #重定向所消耗的时间
c.getinfo(pycurl.SIZE_UPLOAD)    #上传数据包大小
c.getinfo(pycurl.SIZE_DOWNLOAD)    #下载数据包大小
c.getinfo(pycurl.SPEED_DOWNLOAD)    #平均下载速度
c.getinfo(pycurl.SPEED_UPLOAD)    #平均上传速度
c.getinfo(pycurl.HEADER_SIZE)    #HTTP头部大小

我们利用libcurl包提供的这些常量值来达到探测Web服务质量的目的。
</pre>


实现探测Web服务质量

```
#!/usr/bin/env python
#-*- coding:utf-8 -*-

import os,sys,time
import pycurl

URL = "http://jqlinux.com"   #探测的目标URL
c = pycurl.Curl()                 #创建一个Curl对象
c.setopt(pycurl.URL,URL)          #定义请求的URL常量
c.setopt(pycurl.CONNECTTIMEOUT,5) #定义请求连接的等待时间
c.setopt(pycurl.TIMEOUT,5)        #定义请求超时时间
c.setopt(pycurl.NOPROGRESS,1)     #屏蔽下载进度条
c.setopt(pycurl.FORBID_REUSE,1)  #完成交互后强制断开连接，不重用
c.setopt(pycurl.MAXREDIRS,1)     #指定HTTP重定向的最大数为1
c.setopt(pycurl.DNS_CACHE_TIMEOUT,30)  #设置保存DNS信息的时间为30秒
#创建一个文件对象，以”wb”方式打开，用来存储返回的http头部及页面内容
indexfile = open(os.path.dirname(os.path.realpath(__file__))+"/content.txt", "wb")
c.setopt(pycurl.WRITEHEADER, indexfile)    #将返回的HTTP HEADER定向到indexfile文件对象
c.setopt(pycurl.WRITEDATA, indexfile)    #将返回的HTML内容定向到indexfile文件对象
try:
    c.perform()    #提交请求
except Exception,e:
    print "connecion error:"+str(e)
    indexfile.close()
    c.close()
sys.exit()

NAMELOOKUP_TIME =  c.getinfo(c.NAMELOOKUP_TIME)    #获取DNS解析时间
CONNECT_TIME =  c.getinfo(c.CONNECT_TIME)    #获取建立连接时间
PRETRANSFER_TIME =   c.getinfo(c.PRETRANSFER_TIME)    #获取从建立连接到准备传输所消
                                                      #耗的时间
STARTTRANSFER_TIME = c.getinfo(c.STARTTRANSFER_TIME)    #获取从建立连接到传输开始消
                                                        #耗的时间
TOTAL_TIME = c.getinfo(c.TOTAL_TIME)    #获取传输的总时间
HTTP_CODE =  c.getinfo(c.HTTP_CODE)    #获取HTTP状态码
SIZE_DOWNLOAD =  c.getinfo(c.SIZE_DOWNLOAD)    #获取下载数据包大小
HEADER_SIZE = c.getinfo(c.HEADER_SIZE)    #获取HTTP头部大小
SPEED_DOWNLOAD=c.getinfo(c.SPEED_DOWNLOAD)    #获取平均下载速度
#打印输出相关数据
print "HTTP状态码：%s" %(HTTP_CODE)
print "DNS解析时间：%.2f ms"%(NAMELOOKUP_TIME*1000)
print "建立连接时间：%.2f ms" %(CONNECT_TIME*1000)
print "准备传输时间：%.2f ms" %(PRETRANSFER_TIME*1000)
print "传输开始时间：%.2f ms" %(STARTTRANSFER_TIME*1000)
print "传输结束总时间：%.2f ms" %(TOTAL_TIME*1000)
print "下载数据包大小：%d bytes/s" %(SIZE_DOWNLOAD)
print "HTTP头部大小：%d byte" %(HEADER_SIZE)
print "平均下载速度：%d bytes/s" %(SPEED_DOWNLOAD)
#关闭文件及Curl对象
indexfile.close()
c.close()

```