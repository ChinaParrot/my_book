# Python列表（list）

序列是Python中最基本的数据结构。序列中的每个元素都分配一个数字 – 它的位置，或索引，第一个索引是0，第二个索引是1，依此类推。

```
list的方法：
L.append(var) #追加元素
L.insert(index,var) #插入指定的位置
L.pop(var) #返回最后一个元素，并从list中删除之
L.remove(var) #删除第一次出现的该元素
L.count(var) #该元素在列表中出现的个数
L.index(var) #该元素的位置，无责抛出异常
L.extend(list) #追加list,即合并list到L上
L.sort() #排序
L.reverse() #倒叙

a[1:] #片段操作符，用于子list的提取
[1,2]+[3,4] #为[1,2,3,4]。同extend()
[2]*4 #为[2,2,2,2]

#
list[start:end:step]


del L[1] #删除指定下标的元素
del L[1:3] #指定范围

list[start:end:step]


#查看ASCII的值
ord('a')
```

**实例：**

```
#!/usr/bin/env python3
#-*- coding:utf-8 -*-

name = ['a','b',2,'c','d',2,'s','ssss',1,3,5,2,20]
first_pos = 0
for i in range(name.count(2)):
    new_list = name[first_pos:]
    next_pos = new_list.index(2) + 1
    print ('Find postion:',first_pos + new_list.index(2))
    first_pos += next_pos

pos = 0
for y in range(name.count(2)):
    if pos == 0:
       pos = name.index(2)
    else:
        pos = name.index(2,pos + 1)
        print (pos)
```

```
#01
#!/usr/bin/python3
list1 = ['physics', 'chemistry', 1997, 2000];
list2 = [1, 2, 3, 4, 5, 6, 7 ];
print ("list1[0]: ", list1[0])
print ("list2[1:5]: ", list2[1:5])

#结果
list1[0]: physics
list2[1:5]: [2, 3, 4, 5]

#02
#!/usr/bin/python3
list = ['physics', 'chemistry', 1997, 2000];
print ("Value available at index 2 : ")
print (list[2])
list[2] = 2001
print ("New value available at index 2 : ")
print (list[2])

#结果
Value available at index 2 :
1997
New value available at index 2 :
2001

#03
#!/usr/bin/python3
list1 = ['physics', 'chemistry', 1997, 2000];
print list1;
del list1[2];
print ("After deleting value at index 2 : ")
print (list1);
```

**追加元素:**

```
list.append(x)方法

获取列表长度：

len(x)

除了 将元素追加到list中，还能够将两个list合并，或者说将一个list追加到另外一个list中。

ist.extend(L)
```

```
>>> la
[1, 2, 3]
>>> lb
['qiwsir', 'python']
>>> la.extend(lb)
>>> la
[1, 2, 3, 'qiwsir', 'python']
>>> lb
['qiwsir', 'python']
```

**list中某元素的个数:**

上面的len\(L\)，可得到list的长度，也就是list中有多少个元素。python的list还有一个操作，就是数一数某个元素在该list中出现多少次，也就是某个元素有多少个。

list.count\(x\)

可以将list中的元素，从左向右依次从0开始编号，建立索引:

list.index\(x\)，x是list中的一个元素，这样就能够检索到该元素在list中的位置了。这才是真正的索引，注意那个英文单词index。

与list.append\(x\)类似，list.insert\(i,x\)也是对list元素的增加。只不过是可以在任何位置增加一个元素。

list.insert\(i, x\) i是位置，x是增加内容。

list中的元素，不仅能增加，还能被删除，list.pop\(\[i\]\)与list.remove\(x\)，注意看上面的描述。这是一个能够删除list元素的方法，同时上面说明告诉我们，如果x没有在list中，会报错。

list.pop\(x\)\#如果不写x，就如同这个操作，默认删除最后一个，并且将该结果返回

range生成list操作：

range\(start, stop\[, step\]\)是一个内置函数。

1. 这个函数可以创建一个数字元素组成的列表。
2. 这个函数最常用于for循环
3. 函数的参数必须是整数，默认从0开始。返回值是类似\[start, start + step, start + 2\*step, ...\]的列表。
4. step默认值是1。如果不写，就是按照此值。
5. 如果step是正数，返回list的最最后的值不包含stop值，即start+i step这个值小于stop；如果step是负数，start+i step的值大于stop。
6. step不能等于零，如果等于零，就报错。

```
>>> range(9) #stop=9，别的都没有写，含义就是range(0,9,1)
[0, 1, 2, 3, 4, 5, 6, 7, 8] #从0开始，步长为1,增加，直到小于9的那个数
>>> range(0,9)
[0, 1, 2, 3, 4, 5, 6, 7, 8]
>>> range(0,9,1)
[0, 1, 2, 3, 4, 5, 6, 7, 8]

>>> range(1,9) #start=1
[1, 2, 3, 4, 5, 6, 7, 8]

>>> range(0,9,2) #step=2,每个元素等于start+i*step，
[0, 2, 4, 6, 8]
```

如果是从0开始，步长为1,可以写成range\(9\)的样子，但是，如果步长为2，写成range\(9,2\)的样子，计算机就有点糊涂了，它会认为start=9 ,stop=2。所以，在步长不为1的时候，切忌，要把start的值也写上。

start=0,step=2,stop=9.list中的第一个值是start=0,第二个值是start+1 step=2（注意，这里是1，不是2，不要忘记，前面已经讲过，不论是list还是str，对元素进行编号的时候，都是从0开始的），第n个值就是start+\(n-1\) step。直到小于stop前的那个值。





