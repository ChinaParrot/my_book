Python 编程中 while 语句用于循环执行程序，即在某条件下，循环执行某段程序，以处理需要重复处理的相同任务。其基本形式为：

while 判断条件：

执行语句……

例子：

```
#!/usr/bin/python3
count = 0
while (count <20):
    print ('The count is:', count)
    count = count + 2
print ('Good bye!')
```

while 语句时还有另外两个重要的命令 continue，break 来跳过循环，continue 用于跳过该次循环，break 则是用于退出循环，此外"判断条件"还可以是个常值，表示循环必定成立，具体用法如下：

```
#!/usr/bin/python
# -*- coding: UTF-8 -*-
i = 1
while i < 10:
    i += 1
    if i%2 > 0:
        print (i)
        continue
print ('break')
i = 1
while 1:
    print (i)
    i +=1
    if i >10:
        break
```

以下实例使用了 while 来计算 1 到 100 的总和：

```
#!/usr/bin/env python3
# -*- coding: UTF-8 -*-

n = 100
sum = 0
counter = 1
while counter <= n:
    sum = sum + counter
    counter += 1
print("1 到 %d 之和为: %d" % (n,sum))
```

while 实现死循环

```
#!/usr/bin/env python3
# -*- coding: UTF-8 -*-
var = 1
i = 0
while var == 1:
    num = input("请输入：")
    #i += 1
    i = i + 1
    print ("你第 %s 次输入的是：%s" % (i,num))
print ("bye!!!")



#!/usr/bin/env python3
# -*- coding: UTF-8 -*-
import time
while 1:
    print ('死循环')
    time.sleep(1)
```



