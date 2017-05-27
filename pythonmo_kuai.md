# Python模块

* 模块让你能够有逻辑地组织你的Python代码段。
* 把相关的代码分配到一个 模块里能让你的代码更好用，更易懂。
* 模块也是Python对象，具有随机的名字属性用来绑定或引用。
* 简单地说，模块就是一个保存了Python代码的文件。模块能定义函数，类和变量。模块里也能包含可执行的代码。

例子：

一个叫做aname的模块里的Python代码一般都能在一个叫aname.py的文件中找到。下例是个简单的模块support.py。

```
def print_func( par ):
print "Hello : ", par
return
```

**import 语句**

想使用Python源文件，只需在另一个源文件里执行import语句，语法如下：

```
import module1[, module2[,... moduleN]
```

当解释器遇到import语句，如果模块在当前的搜索路径就会被导入。

搜索路径是一个解释器会先进行搜索的所有目录的列表。如想要导入模块hello.py，需要把命令放在脚本的顶端：

```
#!/usr/bin/python
# -*- coding: UTF-8 -*-
# 导入模块
import support
# 现在可以调用模块里包含的函数了
support.print_func("Zara")
以上实例输出结果：
Hello : Zara
一个模块只会被导入一次，不管你执行了多少次import。这样可以防止导入模块被一遍又一遍地执行。
```

**From…import 语句**

Python的from语句让你从模块中导入一个指定的部分到当前命名空间中。语法如下：

```
from modname import name1[, name2[, ... nameN]]
```

例如，要导入模块fib的fibonacci函数，使用如下语句：

```
from fib import fibonacci
```

这个声明不会把整个fib模块导入到当前的命名空间中，它只会将fib里的fibonacci单个引入到执行这个声明的模块的全局符号表。

**From…import\* 语句**

把一个模块的所有内容全都导入到当前的命名空间也是可行的，只需使用如下声明：

```
from modname import *
```

这提供了一个简单的方法来导入一个模块中的所有项目。然而这种声明不该被过多地使用。





