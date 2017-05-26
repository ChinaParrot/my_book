# for 循环语句

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

## 循环控制语句

循环控制语句可以更改语句执行的顺序。Python支持以下循环控制语句：

| 控制语句 | 描述 |
| --- | --- |
| break语句 | 在语句块执行过程中终止循环，并且跳出整个循环 |
| continue 语句 | 在语句块执行过程中终止当前循环，跳出该次循环，执行下一次循环。 |
| pass 语句 | pass是空语句，是为了保持程序结构的完整性。 |



