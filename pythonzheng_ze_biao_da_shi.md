**Python正则表达式        
**

字符串是编程时涉及到的最多的一种数据结构，对字符串进行操作的需求几乎无处不在。比如判断一个字符串是否是合法的Email地址，虽然可以编程提取@前后的子串，再分别判断是否是单词和域名，但这样做不但麻烦，而且代码难以复用。

正则表达式是一种用来匹配字符串的强有力的武器。它的设计思想是用一种描述性的语言来给字符串定义一个规则，凡是符合规则的字符串，我们就认为它“匹配”了，否则，该字符串就是不合法的。

**re.match函数**

re.match 尝试从字符串的起始位置匹配一个模式，如果不是起始位置匹配成功的话，match\(\)就返回none。

函数语法：

`re.match(pattern, string, flags=0)`

函数参数说明：

| 参数 | 描述 |
| --- | --- |
| pattern | 匹配的正则表达式 |
| string | 要匹配的字符串。 |
| flags | 标志位，用于控制正则表达式的匹配方式，如：是否区分大小写，多行匹配等等。 |

匹配成功re.match方法返回一个匹配的对象，否则返回None。

我们可以使用group\(num\) 或 groups\(\) 匹配对象函数来获取匹配表达式。

| 匹配对象方法 | 描述 |
| --- | --- |
| group\(num=0\) | 匹配的整个表达式的字符串，group\(\) 可以一次输入多个组号，在这种情况下它将返回一个包含那些组所对应值的元组。 |
| groups\(\) | 返回一个包含所有小组字符串的元组，从 1 到 所含的小组号。 |

**实例 1：**

```
#!/usr/bin/env python3
# -*- coding: UTF-8 -*-
import re
print(re.match('www', 'www.jqlinux.com').span()) # 在起始位置匹配
print(re.match('jq', 'www.jqlinux.com')) # 不在起始位置匹配

#以上实例运行输出结果为：
(0, 3)
None
```

**实例 2：**

```
#!/usr/bin/env  python3
import re

line = "Cats are smarter than dogs"
#我们强烈建议使用Python的r前缀，就不用考虑转义的问题了：
matchObj = re.match( r'(.*) are (.*?) .*', line, re.M|re.I)

if matchObj:
    print ("matchObj.group() : ", matchObj.group())
    print ("matchObj.group(1) : ", matchObj.group(1))
    print ("matchObj.group(2) : ", matchObj.group(2))
else:
    print ("No match!!")

#以上实例执行结果如下：

matchObj.group() : Cats are smarter than dogs
matchObj.group(1) : Cats
matchObj.group(2) : smarter
```

**re.search方法**

re.search 扫描整个字符串并返回第一个成功的匹配。

函数语法：

```
re.search(pattern, string, flags=0)
```

函数参数说明：

| 参数 | 描述 |
| --- | --- |
| pattern | 匹配的正则表达式 |
| string | 要匹配的字符串。 |
| flags | 标志位，用于控制正则表达式的匹配方式，如：是否区分大小写，多行匹配等等。 |

匹配成功re.search方法返回一个匹配的对象，否则返回None。

我们可以使用group\(num\) 或 groups\(\) 匹配对象函数来获取匹配表达式。

| 匹配对象方法 | 描述 |
| --- | --- |
| group\(num=0\) | 匹配的整个表达式的字符串，group\(\) 可以一次输入多个组号，在这种情况下它将返回一个包含那些组所对应值的元组。 |
| groups\(\) | 返回一个包含所有小组字符串的元组，从 1 到 所含的小组号。 |

**实例 1：**

```
#!/usr/bin/env python3
# -*- coding: UTF-8 -*-
import re
print (re.search('www', 'www.jqlinux.com').span()) # 在起始位置匹配
print (re.search('com', 'www.jqlinux.com').span()) # 不在起始位置匹配

#以上实例运行输出结果为：
(0, 3)
(11, 14)

```

**实例 2：**

```
#!/usr/bin/python
import re

line = "Cats are smarter than dogs";
searchObj = re.search( r'(.*) are (.*?) .*', line, re.M|re.I)
if searchObj:
    print ("searchObj.group() : ", searchObj.group())
    print ("searchObj.group(1) : ", searchObj.group(1))
    print ("searchObj.group(2) : ", searchObj.group(2))
else:
    print ("Nothing found!!")

#以上实例执行结果如下：
searchObj.group() : Cats are smarter than dogs
searchObj.group(1) : Cats
searchObj.group(2) : smarter
```



