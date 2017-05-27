# Python集合\(set\)

在Python set是基本数据类型的一种集合类型，它有可变集合\(set\(\)\)和不可变集合\(frozenset\)两种。创建集合set、集合set添加、集合删除、交集、并集、差集的操作都是非常实用的方法。

集合的添加有两种常用方法，分别是add和update。

集合add方法：是把要传入的元素做为一个整个添加到集合中，例如：

```
>>> a = set('boy')
>>> a.add('python')
>>> a
set(['y', 'python', 'b', 'o'])
```



