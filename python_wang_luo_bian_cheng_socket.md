**Python 网络编程socket**

python 提供了两个级别访问的网络服务。

低级别的网络服务支持基本的 Socket，它提供了标准的 BSD Sockets API，可以访问底层操作系统Socket接口的全部方法。

高级别的网络服务模块 SocketServer， 它提供了服务器中心类，可以简化网络服务器的开发。

什么是 Socket?

Socket又称"套接字"，应用程序通常通过"套接字"向网络发出请求或者应答网络请求，使主机间或者一台计算机上的进程间可以通讯。

socket\(\)函数

Python 中，我们用 socket（）函数来创建套接字，语法格式如下：

`socket.socket([family[, type[, proto]]])`

参数



1. family: 套接字家族可以使AF\_UNIX或者AF\_INET

2. type: 套接字类型可以根据是面向连接的还是非连接分为SOCK\_STREAM或SOCK\_DGRAM

3. protocol: 一般不填默认为0.

**socket类型**

|socket类型| 描述|
|-|-|
|socket.AF_UNIX|只能够用于单一的Unix系统进程间通信|
|socket.AF_INET|服务器之间网络通信|
|socket.AF_INET6|IPv6|
|socket.SOCK_STREAM|流式socket , for TCP|
|socket.SOCK_DGRAM|数据报式socket , for UDP|
|socket.SOCK_RAW|原始套接字，普通的套接字无法处理ICMP、IGMP等网络报文，而SOCK_RAW可以；其次，SOCK_RAW也可以处理特殊的IPv4报文；此外，利用原始套接字，可以通过IP_HDRINCL套接字选项由用户构造IP头。|
|socket.SOCK_SEQPACKET|可靠的连续数据包服务|
|创建TCP Socket：|s=socket.socket(socket.AF_INET,socket.SOCK_STREAM)|
|创建UDP Socket：|s=socket.socket(socket.AF_INET,socket.SOCK_DGRAM)|





