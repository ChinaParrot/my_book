# if语句


Python 编程中 if 语句用于控制程序的执行，基本形式为：

```
if 判断条件：
执行语句……
else：
执行语句……

#多条件
if 判断条件1:
执行语句1……
elif 判断条件2:
执行语句2……
elif 判断条件3:
执行语句3……
else:
执行语句4……

```
例子：

```

#!/usr/bin/python
# -*- coding: UTF-8 -*-
name = 'python'
if name == 'python':
print 'python'
else:
print 'other'



#!/usr/bin/python
# -*- coding: UTF-8 -*-
name = 'python'
if name == 'python':
print 'python'
elif name == 'python2':
print 'python2'
elif name == 'python3':
print 'python3'
```