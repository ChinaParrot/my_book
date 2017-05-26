## Python 字典

字典\(dictionary\)是除列表以外python之中最灵活的内置数据结构类型。列表是有序的对象结合，字典是无序的对象集合。

两者之间的区别在于：字典当中的元素是通过键来存取的，而不是通过偏移存取。

字典用"{ }"标识。字典由索引\(key\)和它对应的值value组成。

```
#!/usr/bin/python
dict = {}
dict['one'] = "This is one"
dict[2] = "This is two"

tinydict = {'name': 'john','code':6734, 'dept': 'sales'}

print (dict['one'])          # 输出键为'one' 的值
print (dict[2])              # 输出键为 2 的值
print (tinydict)             # 输出完整的字典
print (tinydict.keys())      # 输出所有键
print (tinydict.values())    # 输出所有值
#输出结果为：
This is one
This is two
{'dept': 'sales', 'code': 6734, 'name': 'john'}
['dept', 'code', 'name']
['sales', 6734, 'john']
```

**删除字典**

```
tinydict = {'name': 'john','code':6734, 'dept': 'sales'}
del tinydict ['name'] # 删除键 'name'
tinydict .clear()     # 删除字典
del tinydict # 删除字典
```

**字典键的特性**

字典值可以没有限制地取任何python对象，既可以是标准的对象，也可以是用户定义的，但键不行。

两个重要的点需要记住：

1）不允许同一个键出现两次。创建时如果同一个键被赋值两次，后一个值会被记住，如下实例：

```
#!/usr/bin/python3
dict = {'Name': 'xxx', 'Age': 7, 'Name': '小菜鸟'}
print ("dict['Name']: ", dict['Name'])
```

以上实例输出结果：

```
dict['Name']:  小菜鸟
```

2）键必须不可变，所以可以用数字，字符串或元组充当，而用列表就不行，如下实例：

```
#!/usr/bin/python3

dict = {['Name']: 'xxx', 'Age': 7}

print ("dict['Name']: ", dict['Name'])
```

以上实例输出结果：

```
Traceback (most recent call last):
  File "test.py", line 3, in 
<
module
>

    dict = {['Name']: 'W3CSchool', 'Age': 7}
TypeError: unhashable type: 'list'
```

## 字典内置函数&方法

Python字典包含了以下内置函数：

| 函数及描述 | 实例 |
| :--- | :--- |
| len\(dict\) 计算字典元素个数，即键的总数。 | &gt;&gt;&gt; dict = {'Name': 'xxx', 'Age': 7, 'Class': 'First'}&gt;&gt;&gt; len\(dict\)3 |
| str\(dict\) 输出字典以可打印的字符串表示。 | &gt;&gt;&gt; dict = {'Name': 'xxx', 'Age': 7, 'Class': 'First'}&gt;&gt;&gt; str\(dict\)"{'Name': 'xxx', 'Class': 'First', 'Age': 7}" |
| type\(variable\) 返回输入的变量类型，如果变量是字典就返回字典类型。 | &gt;&gt;&gt; dict = {'Name': 'xxx', 'Age': 7, 'Class': 'First'}&gt;&gt;&gt; type\(dict\)&lt;class 'dict'&gt; |

Python字典包含了以下内置方法：

| 函数及描述 |
| :--- |
| [radiansdict.clear\(\)](https://www.w3cschool.cn/python3/python3-att-dictionary-clear.html) 删除字典内所有元素 |
| [radiansdict.copy\(\)](https://www.w3cschool.cn/python3/python3-att-dictionary-copy.html) 返回一个字典的浅复制 |
| [radiansdict.fromkeys\(\)](https://www.w3cschool.cn/python3/python3-att-dictionary-fromkeys.html) 创建一个新字典，以序列seq中元素做字典的键，val为字典所有键对应的初始值 |
| [radiansdict.get\(key, default=None\)](https://www.w3cschool.cn/python3/python3-att-dictionary-get.html) 返回指定键的值，如果值不在字典中返回default值 |
| [key in dict](https://www.w3cschool.cn/python3/python3-att-dictionary-in.html) 如果键在字典dict里返回true，否则返回false |
| [radiansdict.items\(\)](https://www.w3cschool.cn/python3/python3-att-dictionary-items.html) 以列表返回可遍历的\(键, 值\) 元组数组 |
| [radiansdict.keys\(\)](https://www.w3cschool.cn/python3/python3-att-dictionary-keys.html) 以列表返回一个字典所有的键 |
| [radiansdict.setdefault\(key, default=None\)](https://www.w3cschool.cn/python3/python3-att-dictionary-setdefault.html) 和get\(\)类似, 但如果键不存在于字典中，将会添加键并将值设为default |
| [radiansdict.update\(dict2\)](https://www.w3cschool.cn/python3/python3-att-dictionary-update.html) 把字典dict2的键/值对更新到dict里 |
| [radiansdict.values\(\)](https://www.w3cschool.cn/python3/python3-att-dictionary-values.html) 以列表返回字典中的所有值 |



