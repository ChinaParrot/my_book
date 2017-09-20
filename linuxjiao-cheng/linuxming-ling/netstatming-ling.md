netstat -rn ：显示当前系统路由信息

netstat -tlnpu ：显示当前已经启动网络连接和对应的端口信息

netstat -atunp：当前系统上处于网络连接状态的资源信息

netstat -nat ：当前所有端口的网络连接的状态\(tcp协议\)

netstat -an: 当前所有端口的网络连接的状态\(tcp协议 udp协议 系统的端口  ALL\)



netstat -nat

         close：无连接是活动的或正在进行

         listen：服务器在等待进入呼叫

         syn\_recy：一个连接请求已经到达，等待确认

         syn\_sent：应用已经开始，打开一个连接

         established:正常数据传输状态，他的值也可以近似理解为当前服务器的并发数

         fin\_wait1:应用说它已经完成

         fin\_wait2:另一边已同意释放

         itmed\_wait：等待所有分组死掉

         closing:两边同时尝试关闭

         time\_wait：另一边已初始化一个释放

         last\_ack：等待所有分组死掉





netstat -nat \|grep -i "80"

查看80端口的链接状态

netstat -nat\|grep ':80\&gt;'

