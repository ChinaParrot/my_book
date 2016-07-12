# Python集合(set)

在Python set是基本数据类型的一种集合类型，它有可变集合(set())和不可变集合(frozenset)两种。创建集合set、集合set添加、集合删除、交集、并集、差集的操作都是非常实用的方法。


集合的添加有两种常用方法，分别是add和update。

集合add方法：是把要传入的元素做为一个整个添加到集合中，例如：
<pre>
>>> a = set('boy')
>>> a.add('python')
>>> a
set(['y', 'python', 'b', 'o'])
</pre>

集合update方法：是把要传入的元素拆分，做为个体传入到集合中，例如：

<pre>>>> a = set('boy')
>>> a.update('python')
>>> a
set(['b', 'h', 'o', 'n', 'p', 't', 'y'])
</pre>

集合删除操作方法：remove
<pre>
set(['y', 'python', 'b', 'o'])
>>> a.remove('python')
>>> a
set(['y', 'b', 'o'])

</pre>


python set() 集合操作符号、数学符号:
基本操作
<pre>
>>> x = set("jihite")
>>> y = set(['d', 'i', 'm', 'i', 't', 'e'])
>>> x       #把字符串转化为set，去重了
set(['i', 'h', 'j', 'e', 't'])
>>> y
set(['i', 'e', 'm', 'd', 't'])
>>> x & y   #交
set(['i', 'e', 't'])
>>> x | y   #并
set(['e', 'd', 'i', 'h', 'j', 'm', 't'])
>>> x - y   #差
set(['h', 'j'])
>>> y - x
set(['m', 'd'])
>>> x ^ y   #对称差：x和y的交集减去并集
set(['d', 'h', 'j', 'm'])
</pre>

函数操作
<pre>
>>> x
set(['i', 'h', 'j', 'e', 't'])
>>> s = set("hi")
>>> s
set(['i', 'h'])
>>> len(x)                    #长度
>>> 'i' in x
True
>>> s.issubset(x)             #s是否为x的子集
True
>>> y
set(['i', 'e', 'm', 'd', 't'])
>>> x.union(y)                #交
set(['e', 'd', 'i', 'h', 'j', 'm', 't'])
>>> x.intersection(y)         #并
set(['i', 'e', 't'])
>>> x.difference(y)           #差
set(['h', 'j'])
>>> x.symmetric_difference(y) #对称差
set(['d', 'h', 'j', 'm'])
>>> s.update(x)               #更新s，加上x中的元素
>>> s
set(['e', 't', 'i', 'h', 'j'])
>>> s.add(1)                  #增加元素
>>> s
set([1, 'e', 't', 'i', 'h', 'j'])
>>> s.remove(1)               #删除已有元素，如果没有会返回异常
>>> s
set(['e', 't', 'i', 'h', 'j'])
>>> s.remove(2)

Traceback (most recent call last):
  File "<pyshell#29>", line 1, in <module>
    s.remove(2)
KeyError: 2
>>> s.discard(2)               #如果存在元素，就删除；没有不报异常
>>> s
set(['e', 't', 'i', 'h', 'j'])
>>> s.clear()                  #清除set
>>> s
set([])
>>> x
set(['i', 'h', 'j', 'e', 't'])
>>> x.pop()                    #随机删除一元素
'i'
>>> x
set(['h', 'j', 'e', 't'])
>>> x.pop()
'h'
</pre>

#扩展
<pre>
zip拉链

使用zip函数可以把两个列表合并起来，成为一个元组的列表
L1 = [1,3,5,7]
L2 = [2,4,6,8]
#使用zip将两个列表合并
print zip(L1,L2)

for (a,b) in zip(L1,L2):
print (a,b)
L3 = [2,4,6]

#当长度不一的时候，多余的被忽略

print zip(L1,L3)#extra items are ignored

#map则不会忽略，例如下例。当L1和L3长度不一的时候，

#会用第一个参数来填充。
print map(None,L1,L3)
#'zip' a dictionary

#使用zip来造出一个字典。
keys = ['name','age']
values = ['Chen Zhe ',22]
print dict(zip(keys,values))
</pre>