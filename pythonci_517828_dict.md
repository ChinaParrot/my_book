#Python词典(dict)
Python内置了字典：dict的支持，dict全称dictionary，在其他语言中也称为map，使用键-值（key-value）存储，具有极快的查找速度。与列表相似，词典也可以储存多个元素。这种储存多个元素的对象称为容器(container)。

* 
D.get(key,0) #同dict[key],多了没用则返回缺省值，0。[]没用抛出异常
D.has_key(key) #有该键返回true,否则false
D.keys() #返回字典键的列表
D.values() #以列表的形式返回字典中的值，返回值的列表中可包含重复元素。
D.items() #将所有的字典项以列表方式返回，这些列表中的每一项都来与(键，值)，但是项在返回时并没有特殊的顺序。

D.update[dict2] #增加合并字典
D.popitem() #得到一个pair，并从字典中删除它。已空则抛出异常
D.clear() #清空字典，同del dict
D.cmp(dict1,dict2) #比较字典（优先级为元素个数，键大小，键值得大小），第一个大返回1，小返回-1，一样返回0

dict1 = dict #别名
dict2 = dict.copy() #克隆。
dict3 = dict.append() #

例如：

```>>> dic = {'tom':11, 'sam':57,'lily':100}```

```>>> print dic```

```{'lily': 100, 'sam': 57, 'tom': 11}```

```>>> print type(dic)```

```<type 'dict'>```

```>>> ```

```>>> dic['tom']```

```11```

```>>> dic['tom'] = 30```

``` >>> print dic```

```{'lily': 100, 'sam': 57, 'tom': 30}```

```>>> ```

```>>> dic = {'a':1,'b':2,'c':3}```

``` >>> print dic```

```{'a': 1, 'c': 3, 'b': 2}```

``` >>> for key in dic:```

```...     print dic[key]```

```... ```

```1
3
2
>>> ```

通过print的结果，我们可以再次确认，dic中的元素是没有顺序的。

词典的常用方法

print dic.keys() # 返回dic所有的键

print dic.values() # 返回dic所有的值 

print dic.items() # 返回dic所有的元素（键值对）

dic.clear() # 清空dic，dict变为{}

del dic['a'] #删除dic中的a元素
dic.pop('a) #删除指定的元素


词典值得循环：
<pre>
name_info={
    'name':'zhangsan',
    'age':20,
    'job':'Engineer',
    'salary':33333,
    'address':'BJ'
    'gender' :'Male'
}
for i in name_info:
    print i,name_info[i]
    
#或者

for k,v in name_info.items():
    print k,v
    
</pre>
