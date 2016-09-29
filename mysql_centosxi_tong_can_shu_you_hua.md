 #MySQL centos系统层优化
 
### 内核优化添加 /etc/sysctl.conf


```
kernel.msgmnb = 65536
kernel.msgmax = 65536
kernel.shmmax = 68719476736
kernel.shmall = 4294967296
net.core.somaxconn = 65535
net.core.netdev_max_backlog = 65535
net.ipv4.tcp_max_syn_backlog = 65535
net.ipv4.tcp_fin_timeout = 10
net.ipv4.tcp_tw_reuse = 1
net.ipv4.tcp_tw_recycle = 1
net.core.wmem_default = 87380
net.core.wmem_max = 16777216
net.core.rmem_default = 87380
net.core.rmem_max = 16777216

```

###打开文件数优化


增加资源限制（/etc/secuity/limit.conf）

```
* soft nofile 65535
* hard nofile 65535

```
###磁盘调度策略

```
cat /sys/block/sda/queue/scheduler 
noop anticipatory deadline [cfq] 

```

* noop(电梯式调度策略)
 NOOP 实现了一个FIFO队列，它像电梯的工作方法一样对I/O请求进行组织，当有一个新的请求到来时，它将请求合并到最近的请求之后，以此来保证请求同一个介质。NOOP倾向饿死读而不利于写，因此NOOP对于闪存设备、RAM及嵌入式是最好的选择。

* cfq

CFQ实现了一种QoS的IO调度算法。该算法为每一个进程分配一个时间窗口，在该时间窗口内，允许进程发出IO请求。通过时间窗口在不同进程间的移动，保证了对于所有进程而言都有公平的发出IO请求的机会。同时CFQ也实现了进程的优先级控制，可保证高优先级进程可以获得更长的时间窗口。

CFQ适用于系统中存在多任务I/O请求的情况，通过在多进程中轮换，保证了系统I/O请求整体的低延迟。但是，对于只有少数进程存在大量密集的I/O请求的情况，会出现明显的I/O性能下降。


###对文件系统对性能的影响

EXT3/4 系统的挂载参数 （/etc/fstab）

data =writeback | ordered |journal|noatime,nodiratime

/dev/sda1/ext4 noatime,nodiratime,data=writeback 1 1

