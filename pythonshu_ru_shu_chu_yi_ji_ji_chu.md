#Python输入输出以及基础

##输出
用print()在括号中加上字符串，就可以向屏幕上输出指定的文字。比如输出'hello, world'，用代码实现如下：

 ```print ('hello, world')```
 
print语句也可以跟上多个字符串，用逗号“,”隔开，就可以连成一串输出：
 
```
print ('The quick brown fox', 'jumps over', 'the lazy dog')
#结果
The quick brown fox jumps over the lazy dog
```

##输入

现在，你已经可以用print()输出你想要的结果了。但是，如果要让用户从电脑输入一些字符怎么办？Python提供了一个input()，可以让用户输入字符串，并存放到一个变量里。比如输入用户的名字：

```name = input()```

##Python注释

python中单行注释采用 # 开头。
```#!/usr/bin/python
# -*- coding: UTF-8 -*-
# 文件名：test.py

# 第一个注释
print ("Hello, Python!")  # 第二个注释
```
python 中多行注释使用三个单引号(''')或三个双引号(""")。
```#!/usr/bin/python
# -*- coding: UTF-8 -*-
# 文件名：test.py


'''
这是多行注释，使用单引号。
这是多行注释，使用单引号。
这是多行注释，使用单引号。
'''

"""
这是多行注释，使用双引号。
这是多行注释，使用双引号。
这是多行注释，使用双引号。
"""```

#一个汉子占用3个字符
<pre>
 >>> name = u"薛";                                                                                   
>>> len(name)
1
>>> name_utf_8=name.encode('utf-8')
>>> len(name_utf_8)
3
>>>name_utf_8.decode('utf-8')
>>>u'\u859b'
 </pre>

##Python 标识符
在python里，标识符有字母、数字、下划线组成。<br />
在python中，所有标识符可以包括英文、数字以及下划线（_），但不能以数字开头。<br />
python中的标识符是区分大小写的。

##Python保留字符
 具有特定意义的字符串，通常也称为保留字。用户定义的标识符不应与关键字相同
 
 | 保留字 |保留字 |保留字 |
| -- | -- | -- |
| assert | finally | or |
| and  | exec | not |
| break | for | pass |
| class | from | print |
| continue | global |raise |
| del | if | return |
| elif | import | try |
| in| while | else |
| is | with | except |
|lambda|yield|def|

##Python 引号

Python 接收单引号(‘ )，双引号(” )，三引号(”’ “””) 来表示字符串，引号的开始与结束必须的相同类型的。

其中三引号可以由多行组成，编写多行文本的快捷语法，常用语文档字符串，在文件的特定地点，被当做注释。


##变量


变量存储在内存中的值。这就意味着在创建变量时会在内存中开辟一个空间。

基于变量的数据类型，解释器会分配指定内存，并决定什么数据可以被存储在内存中。

因此，变量可以指定不同的数据类型，这些变量可以存储整数，小数或字符。


<pre>
counter = 100 # 赋值整型变量
miles = 1000.0 # 浮点型
name = "John" # 字符串

mys = """
aaaa
bbbb
dddd
"""

print counter
print miles
print name
print mys


</pre>

数字类型：

    – int（有符号整型）
    – long（长整型[也可以代表八进制和十六进制]）
    – float（浮点型）
    – complex（复数）
字符串：

字符串或串(String)是由数字、字母、下划线组成的一串字符。

```#!/usr/bin/python

var1 = 'Hello World!'
var2 = "Python Programming"

print "var1[0]: ", var1[0]
print "var2[1:5]: ", var2[1:5]

结果： var1[0]:  H
      var2[1:5]:  ytho```
 
1、 字符串的长度：
 
 len(a)

2、有时候要用到大小写转换：

S.upper() #S中的字母大写<br>
S.lower() #S中的字母小写<br>
S.capitalize() #首字母大写<br>
S.istitle() #单词首字母是否大写的，且其它为小写<br>
S.isupper() #S中的字母是否全是大写<br>
S.islower() #S中的字母是否全是小写

<pre>
#请写一个字符串转成驼峰的方法？
def convert(one_string,space_character):    #one_string:输入的字符串；space_character:字符串的间隔符，以其做为分隔标志
    string_list = str(one_string).split(space_character)    #将字符串转化为list
    first = string_list[0].lower()
    others = string_list[1:] 
    others_capital = [word.capitalize() for word in others]      #str.capitalize():将字符串的首字母转化为大写
    others_capital[0:0] = [first]
    hump_string = ''.join(others_capital)     #将list组合成为字符串，中间无连接符。
    return hump_string
if __name__=='__main__':
    print "the string is:ab-cd-ef"
    print "convert to hump:"
    print convert("ab-cd-ef","-")
</pre>


3、去掉字符串左右空格

S.strip() 去掉字符串的左右空格

S.lstrip() 去掉字符串的左边空格

S.rstrip() 去掉字符串的右边空格


##python运算符
Python算术运算符

以下假设变量a为10，变量b为20：

| 运算符 | 描述 | 实例|
| -- | -- | -- |
| + |加 – 两个对象相加 | a + b 输出结果 30 |
| – | 减 – 得到负数或是一个数减去另一个数 |a – b 输出结果 -10 |
| * | 乘 – 两个数相乘或是返回一个被重复若干次的字符串 | 	a * b 输出结果 200 |
| / | 除 – x除以y | b / a 输出结果 2 |
|%  |取模 – 返回除法的余数|b % a 输出结果 0|
|** |幂 – 返回x的y次幂|a**b 为10的20次方， 输出结果 100000000000000000000|
|// |取整除 – 返回商的整数部分|9//2 输出结果 4 , 9.0//2.0 输出结果 4.0|


##python赋值运算符

| 运算符 | 描述 | 实例 |
| -- | -- | -- |
| = | 简单的赋值运算符 | c = a + b 将 a + b 的运算结果赋值为 c |
| +=| 加法赋值运算符 | c += a 等效于 c = c + a |
| -= | 减法赋值运算符 | c -= a 等效于 c = c – a |
| *= | 乘法赋值运算符 |c *= a 等效于 c = c * a |
|/=|除法赋值运算符|c /= a 等效于 c = c / a|
|%=|取模赋值运算符|c %= a 等效于 c = c % a|
|**=|幂赋值运算符|c **= a 等效于 c = c ** a|
|//=|取整除赋值运算符|c //= a 等效于 c = c // a|

##Python比较运算符
以下假设变量a为10，变量b为20：

| 运算符	 | 描述 | 实例|
| -- | -- | -- |
| == | 等于 – 比较对象是否相等 | (a == b) 返回 False |
|!=	|不等于 – 比较两个对象是否不相等|	(a != b) 返回 true|
|<>	|不等于 – 比较两个对象是否不相等|	(a <> b) 返回 true这个运算符类似 !=|
|>	|大于 – 返回x是否大于y	|(a > b) 返回 False|
|<	|小于 – 返回x是否小于y。所有比较运算符返回1表示真，返回0表示假。这分别与特殊的变量True和False等价。注意，这些变量名的大写。|	(a < b) 返回 true|
|>=	|大于等于 – 返回x是否大于等于y|	(a >= b) 返回 False|
|<=	|小于等于 – 返回x是否小于等于y|	(a <= b) 返回 true|

##Python逻辑运算符

Python语言支持逻辑运算符，以下假设变量a为10，变量b为20：

|运算符|	描述|	实例|
|--|--|--|
|and|	布尔”与” – 如果x为False，x and y返回False，否则它返回y的计算值|	(a and b) 返回 true|
|or	|布尔”或” – 如果x是True，它返回True，否则它返回y的计算值|	(a or b) 返回 true|
|not|布尔”非” – 如果x为True，返回False。如果x为False，它返回True|	not(a and b) 返回 false|

##Python成员运算符
除了以上的一些运算符之外，Python还支持成员运算符，测试实例中包含了一系列的成员，包括字符串，列表或元组。

|运算符	|描述	|实例|
|--|--|--|
|in	|如果在指定的序列中找到值返回True，否则返回False。|	x 在 y序列中 , 如果x在y序列中返回True。|
|not in	|如果在指定的序列中没有找到值返回True，否则返回False。|	x 不在 y序列中 , 如果x不在y序列中返回True。|

##python转义字符
在需要在字符中使用特殊字符时，python用反斜杠(\)转义字符。如下表：

|转义字符|	描述|
|--|--|
|\\(在行尾时)|	续行符|
|\\\|	反斜杠符号|
|\’|	单引号|
|\”|	双引号|
|\a|	响铃|
|\b|	退格(Backspace)|
|\e|	转义|
|\000|	空|
|\n|	换行|
|\v|	纵向制表符|
|\t|	横向制表符|
|\r|	回车|
|\f|	换页|
|\oyy|	八进制数，yy代表的字符，例如：\o12代表换行|
|\xyy|	十六进制数，yy代表的字符，例如：\x0a代表换行|
|\other|	其它的字符以普通格式输出|

##Python字符串格式化
Python 支持格式化字符串的输出 。尽管这样可能会用到非常复杂的表达式，但最基本的用法是将一个值插入到一个有字符串格式符 %s 的字符串中。

如下实例：

```
#!/usr/bin/python

print "My name is %s and weight is %d kg!" % ('Zara', 21)
#结果
My name is Zara and weight is 21 kg!
```
python字符串格式化符号:

      %c	 格式化字符及其ASCII码
      %s	 格式化字符串
      %d	 格式化整数
      %u	 格式化无符号整型
      %o	 格式化无符号八进制数
      %x	 格式化无符号十六进制数
      %X	 格式化无符号十六进制数（大写）
      %f	 格式化浮点数字，可指定小数点后的精度
      %e	 用科学计数法格式化浮点数
      %E	 作用同%e，用科学计数法格式化浮点数
      %g	 %f和%e的简写
      %G	 %f 和 %E 的简写
      %p	 用十六进制数格式化变量的地址
      

