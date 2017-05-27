# Python日期时间

datetime是Python处理日期和时间的标准库。

Python程序能用很多方式处理日期和时间。转换日期格式是一个常见的例行琐事。Python有一个 time 和 calendar 模组可以帮忙。

```
#time 获取当前时间
#!/usr/bin/python
import time;

localtime = time.localtime(time.time())
print "Local current time :", localtime

#结果
time.struct_time(tm_year=2016, tm_mon=2, tm_mday=25, tm_hour=22, tm_min=48, tm_sec=27, tm_wday=3, tm_yday=56, tm_isdst=0)

localtime = time.asctime( time.localtime(time.time()) )
print "Local current time :", localtime

#结果
Local current time : Thu Feb 25 22:50:47 2016
```



