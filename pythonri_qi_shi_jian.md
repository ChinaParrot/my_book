# Python日期时间

datetime是Python处理日期和时间的标准库。

Python程序能用很多方式处理日期和时间。转换日期格式是一个常见的例行琐事。Python有一个 time 和 calendar 模组可以帮忙。

**format time结构化表示**

| **格式** |
| :--- |


|  | **含义** |
| :--- | :--- |
| %a | 本地（locale）简化星期名称 |
| %A | 本地完整星期名称 |
| %b | 本地简化月份名称 |
| %B | 本地完整月份名称 |
| %c | 本地相应的日期和时间表示 |
| %d | 一个月中的第几天（01 - 31） |
| %H | 一天中的第几个小时（24小时制，00 - 23） |
| %I | 第几个小时（12小时制，01 - 12） |
| %j | 一年中的第几天（001 - 366） |
| %m | 月份（01 - 12） |
| %M | 分钟数（00 - 59） |
| %p | 本地am或者pm的相应符 |
| %S | 秒（01 - 61） |
| %U | 一年中的星期数。（00 - 53星期天是一个星期的开始。）第一个星期天之前的所有天数都放在第0周。 |
| %w | 一个星期中的第几天（0 - 6，0是星期天） |
| %W | 和%U基本相同，不同的是%W以星期一为一个星期的开始。 |
| %x | 本地相应日期 |
| %X | 本地相应时间 |
| %y | 去掉世纪的年份（00 - 99） |
| %Y | 完整的年份 |
| %Z | 时区的名字（如果不存在为空字符） |
| %% | ‘%’字符 |

**time**

```
#!/usr/bin/env python3
import time
#如函数time.time()用于获取当前时间戳
print (time.time())
#时间结构
localtime = time.localtime()
#但是最简单的获取可读的时间模式的函数是asctime()
localtime2 =time.asctime(time.localtime())

print (localtime)
print (localtime2)
print (time.strftime("%Y-%m-%d %X"))


#结果

1495859168.1940289
time.struct_time(tm_year=2017, tm_mon=5, tm_mday=27, tm_hour=12, tm_min=26, tm_sec=8, tm_wday=5, tm_yday=147, tm_isdst=0)
Sat May 27 12:26:08 2017
2017-05-27 13:53:47
[Finished in 0.3s]
```

**datetime**

```
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
```

注意到datetime是模块，datetime模块还包含一个datetime类，通过from datetime import datetime导入的才是datetime这个类。

如果仅导入import datetime，则必须引用全名datetime.datetime。

datetime.now\(\)返回当前日期和时间，其类型是datetime。

```
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
```

```
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
```

**datetime加减                  
**

对日期和时间进行加减实际上就是把datetime往后或往前计算，得到新的datetime。加减可以直接用+和-运算符，不过需要导入timedelta这个类：

```
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
```

**本地时间转换为UTC时间**

本地时间是指系统设定时区的时间，例如北京时间是UTC+8:00时区的时间，而UTC时间指UTC+0:00时区的时间。

```
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
```

**日历**

```
#!/usr/bin/python
import calendar

cal = calendar.month(2016, 5)
print "Here is the calendar:"
print cal
```



