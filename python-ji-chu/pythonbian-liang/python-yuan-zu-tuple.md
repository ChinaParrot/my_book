## Python元组

元组是另一个数据类型，类似于List（列表）。

元组用"\(\)"标识。内部元素用逗号隔开。但是元组不能二次赋值，相当于只读列表。

```
#!/usr/bin/python
# -*- coding: UTF-8 -*-

tuple = ( 'xxx', 786 , 2.23, 'john', 70.2 )
tinytuple = (123, 'john')

print (tuple)               # 输出完整元组
print (tuple[0])            # 输出元组的第一个元素
print (tuple[1:3])          # 输出第二个至第三个的元素 
print (tuple[2:])           # 输出从第三个开始至列表末尾的所有元素
print (tinytuple * 2)       # 输出元组两次
print (tuple + tinytuple)   # 打印组合的元组

#结果
'xxx', 786, 2.23, 'john', 70.2)
xxx
(786, 2.23)
(2.23, 'john', 70.2)
(123, 'john', 123, 'john')
('xxx', 786, 2.23, 'john', 70.2, 123, 'john')
```

以下是元组无效的，因为元组是不允许更新的。而列表是允许更新的：

```
#!/usr/bin/python
# -*- coding: UTF-8 -*-

tuple = ( 'xxx', 786 , 2.23, 'john', 70.2 )
list = [ 'xxx', 786 , 2.23, 'john', 70.2 ]
tuple[2] = 1000    # 元组中是非法应用
list[2] = 1000     # 列表中是合法应用
```

但我们可以对元组进行连接组合，如下实例:

```
#!/usr/bin/python3

tup1 = (12, 34.56);
tup2 = ('abc', 'xyz')

# 以下修改元组元素操作是非法的。
# tup1[0] = 100

# 创建一个新的元组
tup3 = tup1 + tup2;
print (tup3)

#以上实例输出结果：

(12, 34.56, 'abc', 'xyz')
```

**删除元组**

元组中的元素值是不允许删除的，但我们可以使用del语句来删除整个元组，如下实例:

```
#!/usr/bin/python3

tup = ('Google', 'xxx', 1997, 1997)

print (tup)
del tup;
print ("删除后的元组 tup : ")
print (tup)
```

**元组内置函数**

Python元组包含了以下内置函数

| 方法及描述 | 实例 |
| :--- | :--- |
| len\(tuple\) 计算元组元素个数。 | &gt;&gt;&gt; tuple1 = \('Google', 'W3CSchool', 'Taobao'\)&gt;&gt;&gt; len\(tuple1\)3&gt;&gt;&gt; |
| max\(tuple\) 返回元组中元素最大值。 | &gt;&gt;&gt; tuple2 = \('5', '4', '8'\)&gt;&gt;&gt; max\(tuple2\)'8'&gt;&gt;&gt; |
| min\(tuple\) 返回元组中元素最小值。 | &gt;&gt;&gt; tuple2 = \('5', '4', '8'\)&gt;&gt;&gt; min\(tuple2\)'4'&gt;&gt;&gt; |
| tuple\(seq\) 将列表转换为元组。 | &gt;&gt;&gt; list1= \['Google', 'Taobao', 'W3CSchool', 'Baidu'\]&gt;&gt;&gt; tuple1=tuple\(list1\)&gt;&gt;&gt; tuple1\('Google', 'Taobao', 'W3CSchool', 'Baidu'\) |



