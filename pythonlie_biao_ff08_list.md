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



