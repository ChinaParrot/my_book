``---#Python语句汇总

## 一、if语句

Python 编程中 if 语句用于控制程序的执行，基本形式为：<br />


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

## 二、While循环语句
Python 编程中 while 语句用于循环执行程序，即在某条件下，循环执行某段程序，以处理需要重复处理的相同任务。其基本形式为：<br />

<pre>while 判断条件：
    执行语句……</pre>

例子：<br>

``` 
#!/usr/bin/python
count = 0
while (count <20):
	print 'The count is:',count
	count = count + 2
print 'Good bye!'

```

while 语句时还有另外两个重要的命令 continue，break 来跳过循环，continue 用于跳过该次循环，break 则是用于退出循环，此外"判断条件"还可以是个常值，表示循环必定成立，具体用法如下：

 ```

#!/usr/bin/python
# -*- coding: UTF-8 -*-
print 'continue'
i = 1
while i < 10:
  i +=1
  if i%2 > 0:
    continue
  print i

print 'break'
i = 1
while 1:
  print i
  i +=1
  if i >10:
    break
 
 
 死循环

 #!/usr/bin/python
 # -*- coding: UTF-8 -*-
import time
while 1:
  print '死循环'
  time.sleep(1)

```


循环使用 else 语句

```

#!/usr/bin/python
# -*- coding: UTF-8 -*-
count = 0
while count <6:
  print count,"is less than 5"
  count += 1
else:
  print count,"is not less than 5"

```


##三、for 循环语句


Python for循环可以遍历任何序列的项目，如一个列表或者一个字符串。
语法：<br>
for循环的语法格式如下：

 <pre>for iterating_var in sequence:
   statements(s)</pre>

```
#!/usr/bin/python
#-*- coding:UTF-8 -*-

for letter in 'abcdefg':
	print '当前字母：',letter
fruits = ['banana', 'apple',  'mango']
for fruit in fruits:
	   print '当前水果 :', fruit
print "Good bye!"

```


另外一种执行循环的遍历方式是通过索引，如下实例：

```

#!/usr/bin/python
# -*- coding: UTF-8 -*-

fruits = ['banana', 'apple',  'mango']
for index in range(len(fruits)):
   print '当前水果 :', fruits[index]

print "Good bye!"

```


循环使用 else 语句：

```

#!/usr/bin/python
#-*- coding:UTF-8 -*-

for num in range(10,20):
  for i in range(2,num):
     if num%i == 0:
	  j = num /i
	  print '%d 等于 %d * %d' %(num,i,j)
	  break
  else:
     print num,'是一个质数'

```
##循环控制语句

循环控制语句可以更改语句执行的顺序。Python支持以下循环控制语句：

|控制语句|描述|
|--|--|
|break语句|在语句块执行过程中终止循环，并且跳出整个循环 |
|continue 语句 |在语句块执行过程中终止当前循环，跳出该次循环，执行下一次循环。 |
|pass 语句|pass是空语句，是为了保持程序结构的完整性。 |








 

