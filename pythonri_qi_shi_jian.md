#Python日期时间

datetime是Python处理日期和时间的标准库。

Python程序能用很多方式处理日期和时间。转换日期格式是一个常见的例行琐事。Python有一个 time 和 calendar 模组可以帮忙。

例子：
<pre>
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

</pre>

```

#datetime
>>>print (datetime.now())
2016-05-12 14:55:16.708495
>>> import datetime
>>> n = datetime.datetime.now()
>>> n
datetime.datetime(2016, 5, 12, 15, 23, 2, 433582)
>>> n.timetuple()
time.struct_time(tm_year=2016, tm_mon=5, tm_mday=12, tm_hour=15, tm_min=23, tm_sec=2, tm_wday=3, tm_yday=133, tm_isdst=-1)

>>> t=time.time()
>>> from datetime import datetime
>>> print(datetime.fromtimestamp(t))
2016-05-12 14:50:07.138568
>>> 
注意到datetime是模块，datetime模块还包含一个datetime类，通过from datetime import datetime导入的才是datetime这个类。
如果仅导入import datetime，则必须引用全名datetime.datetime。
datetime.now()返回当前日期和时间，其类型是datetime。

#格式化输出
>>> from datetime import datetime
>>> cday = datetime.strptime('2016-5-12 18:19:59', '%Y-%m-%d %H:%M:%S')
>>> print cday
2016-05-12 18:19:59
>>> 

#datetime转换为str
>>> from datetime import datetime
>>> now = datetime.now()
>>> print(now.strftime('%a, %b %d %H:%M'))
Thu, May 12 15:33
>>> print(now.strftime('%Y-%m-%d %H:%M:%S'))
2016-05-12 15:33:40

#!/usr/bin/python
# -*- coding: UTF-8 -*-
import time
# 格式化成2016-03-20 11:45:39形式
print time.strftime("%Y-%m-%d %H:%M:%S", time.localtime()) 
# 格式化成Sat Mar 28 22:24:24 2016形式
print time.strftime("%a %b %d %H:%M:%S %Y", time.localtime()) 
# 将格式字符串转换为时间戳
a = "Sat Mar 28 22:24:24 2016"
print time.mktime(time.strptime(a,"%a %b %d %H:%M:%S %Y"))

#datetime加减
对日期和时间进行加减实际上就是把datetime往后或往前计算，得到新的datetime。加减可以直接用+和-运算符，不过需要导入timedelta这个类：
>>> from datetime import datetime, timedelta
>>> now = datetime.now()
>>> now
datetime.datetime(2016, 5, 12, 15, 35, 52, 311921)
>>> now + timedelta(hours=10)
datetime.datetime(2016, 5, 13, 1, 35, 52, 311921)
>>> now - timedelta(days=1)
datetime.datetime(2016, 5, 11, 15, 35, 52, 311921)
>>> now + timedelta(days=2, hours=12)
datetime.datetime(2016, 5, 15, 3, 35, 52, 311921)
>>> 

#本地时间转换为UTC时间
本地时间是指系统设定时区的时间，例如北京时间是UTC+8:00时区的时间，而UTC时间指UTC+0:00时区的时间。
import time
import datetime
def utc2local(utc_st):
    “”“UTC时间转本地时间（+8:00）”“”
    now_stamp = time.time()
    local_time = datetime.datetime.fromtimestamp(now_stamp)
    utc_time = datetime.datetime.utcfromtimestamp(now_stamp)
    offset = local_time - utc_time
    local_st = utc_st + offset
    return local_st
def local2utc(local_st):
    “”“本地时间转UTC时间（-8:00）”“”
    time_struct = time.mktime(local_st.timetuple())
    utc_st = datetime.datetime.utcfromtimestamp(time_struct)
    return utc_st
utc_time = datetime.datetime(2014, 9, 18, 10, 42, 16, 126000)
# utc转本地
local_time = utc2local(utc_time)
print local_time.strftime(“%Y-%m-%d %H:%M:%S”)
# output：2014-09-18 18:42:16

# 本地转utc
utc_tran = local2utc(local_time)
print utc_tran.strftime(“%Y-%m-%d %H:%M:%S”)
# output：2014-09-18 10:42:16

#日历
#!/usr/bin/python
import calendar

cal = calendar.month(2016, 5)
print "Here is the calendar:"
print cal;```
