# for 循环语句

|  |
| :--- |


| 循环类型 | 描述 |
| :--- | :--- |
| [while 循环](http://www.runoob.com/python/python-while-loop.html) | 在给定的判断条件为 true 时执行循环体，否则退出循环体。 |
| [for 循环](http://www.runoob.com/python/python-for-loop.html) | 重复执行语句 |
| [嵌套循环](http://www.runoob.com/python/python-nested-loops.html) | 你可以在while循环体中嵌套for循环 |

Python for循环可以遍历任何序列的项目，如一个列表或者一个字符串。  
语法：  
for循环的语法格式如下：

```
for <variable> in <sequence>:
  <statements>
else:
  <statements>
```

```
#!/usr/bin/env python3
#-*- coding:UTF-8 -*-
for letter in 'abcdefg':
    print ('当前字母：',letter)
fruits = ['banana', 'apple', 'mango']
for fruit in fruits:
    print ('当前水果 :', fruit)
print ("Good bye!")
```

另外一种执行循环的遍历方式是通过索引，如下实例：

```
#!/usr/bin/env python3
# -*- coding: UTF-8 -*-

fruits = ['banana', 'apple', 'mango']
for index in range(len(fruits)):
    print ('当前水果 :', fruits[index])
    print ('当前index是：', index)
print ("Good bye!")
```

循环使用 else 语句：

```
#!/usr/bin/env python3
#-*- coding:UTF-8 -*-

for num in range(1,20):
    for i in range(2,num):
        if num%i == 0:
            j = num / i
            print ('%d 等于 %d * %d' %(num,i,j))
            break
    else:
        print (num,'是一个质数')
```

## 循环控制语句

循环控制语句可以更改语句执行的顺序。Python支持以下循环控制语句：

| 控制语句 | 描述 |
| --- | --- |
| break语句 | 在语句块执行过程中终止循环，并且跳出整个循环 |
| continue 语句 | 在语句块执行过程中终止当前循环，跳出该次循环，执行下一次循环。 |
| pass 语句 | pass是空语句，是为了保持程序结构的完整性。 |



