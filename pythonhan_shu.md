# Python 函数

函数是组织好的，可重复使用的，用来实现单一，或相关联功能的代码段。

函数能提高应用的模块性，和代码的重复利用率。你已经知道Python提供了许多内建函数，比如print\(\)。但你也可以自己创建函数，这被叫做用户自定义函数。

定义一个函数

1. 你可以定义一个由自己想要功能的函数，以下是简单的规则：
2. 函数代码块以 def 关键词开头，后接函数标识符名称和圆括号\(\)。
3. 任何传入参数和自变量必须放在圆括号中间。圆括号之间可以用于定义参数。
4. 函数的第一行语句可以选择性地使用文档字符串—用于存放函数说明。
5. 函数内容以冒号起始，并且缩进。
6. return \[表达式\] 结束函数，选择性地返回一个值给调用方。不带表达式的return相当于返回 None。

**语法**

```
def functionname( parameters ):
    "函数_文档字符串"
    function_suite
    return [expression]
```

**函数调用**

定义一个函数只给了函数一个名称，指定了函数里包含的参数，和代码块结构。

这个函数的基本结构完成以后，你可以通过另一个函数调用执行，也可以直接从Python提示符执行。

如下实例调用了printme（）函数：

```
def printme( str ):
    """
    打印传入的字符串
    """
    print (str)
    return
# 调用函数
printme("我要调用用户自定义函数!");
printme("再次调用同一函数");

#以上实例输出结果：

我要调用用户自定义函数!
再次调用同一函数
```

所有参数（自变量）在Python里都是按引用传递。如果你在函数里修改了参数，那么在调用这个函数的函数里，原始的参数也被改变了。例如：

```
#!/usr/bin/env python3
# -*- coding: UTF-8 -*-
# 可写函数说明

def changeme( mylist ):
    "修改传入的列表"
    mylist.append([1,2,3,4]);
    print ("函数内取值: ", mylist)
    return

# 调用changeme函数
mylist = [10,20,30];
changeme( mylist );
print ("函数外取值: ", mylist)
```

**匿名函数**

python 使用 lambda 来创建匿名函数。

lambda只是一个表达式，函数体比def简单很多。

lambda的主体是一个表达式，而不是一个代码块。仅仅能在lambda表达式中封装有限的逻辑进去。

lambda函数拥有自己的命名空间，且不能访问自有参数列表之外或全局命名空间里的参数。

虽然lambda函数看起来只能写一行，却不等同于C或C++的内联函数，后者的目的是调用小函数时不占用栈内存从而增加运行效率。

**语法:**

lambda函数的语法只包含一个语句，如下：

`lambda [arg1 [,arg2,.....argn]]:expression`

如下实例：

```
#!/usr/bin/env python3
# -*- coding: UTF-8 -*-
# 可写函数说明
sum = lambda arg1, arg2: arg1 + arg2;
# 调用sum函数
print ("相加后的值为 : ", sum( 10, 20 ))
print ("相加后的值为 : ", sum( 20, 20 ))


以上实例输出结果：
相加后的值为 : 30
相加后的值为 : 40
```

**return语句**

return语句\[表达式\]退出函数，选择性地向调用方返回一个表达式。不带参数值的return语句返回None。之前的例子都没有示范如何返回数值，下例便告诉你怎么做：

```
#!/usr/bin/env python3
# -*- coding: UTF-8 -*-
# 可写函数说明

def sum( arg1, arg2 ):
    # 返回2个参数的和."
    total = arg1 + arg2
    print ("函数内 : ", total)
    return total;
# 调用sum函数
total = sum( 10, 20 );
print ("函数外 : ", total)
```

**变量作用域**

一个程序的所有的变量并不是在哪个位置都可以访问的。访问权限决定于这个变量是在哪里赋值的

变量的作用域决定了在哪一部分程序你可以访问哪个特定的变量名称。两种最基本的变量作用域如下：

全局变量

局部变量

全局变量和局部变量

定义在函数内部的变量拥有一个局部作用域，定义在函数外的拥有全局作用域。

局部变量只能在其被声明的函数内部访问，而全局变量可以在整个程序范围内访问。调用函数时，所有在函数内声明的变量名称都将被加入到作用域中。如下实例：

```
#!/usr/bin/env python3
# -*- coding: UTF-8 -*-

total = 0; # 这是一个全局变量
# 可写函数说明
def sum( arg1, arg2 ):
    #返回2个参数的和."
    total = arg1 + arg2; # total在这里是局部变量.
    print ("函数内是局部变量 : ", total)
    return total;
#调用sum函数
sum( 10, 20 );
print ("函数外是全局变量 : ", total)
```

**递归函数**

在函数内部，可以调用其他函数。如果一个函数在内部调用自身本身，这个函数就是递归函数。

举个例子，我们来计算阶乘`n! = 1 x 2 x 3 x ... x n`，用函数`fact(n)`表示，可以看出：

所以，`fact(n)`可以表示为`n x fact(n-1)`，只有n=1时需要特殊处理。

于是，`fact(n)`用递归的方式写出来就是：

```
def fact(n):
    if n==1:
        return 1
    return n * fact(n - 1)
print (fact(5))
```

如果我们计算`fact(5)`，可以根据函数定义看到计算过程如下：

```
===> fact(5)
===> 5 * fact(4)
===> 5 * (4 * fact(3))
===> 5 * (4 * (3 * fact(2)))
===> 5 * (4 * (3 * (2 * fact(1))))
===> 5 * (4 * (3 * (2 * 1)))
===> 5 * (4 * (3 * 2))
===> 5 * (4 * 6)
===> 5 * 24
===> 120
```

递归函数的优点是定义简单，逻辑清晰。理论上，所有的递归函数都可以写成循环的方式，但循环的逻辑不如递归清晰。

使用递归函数需要注意防止栈溢出。在计算机中，函数调用是通过栈（stack）这种数据结构实现的，每当进入一个函数调用，栈就会加一层栈帧，每当函数返回，栈就会减一层栈帧。由于栈的大小不是无限的，所以，递归调用的次数过多，会导致栈溢出。可以试试

`fact(1000)`：

```
Traceback (most recent call last):
  File "C:\Users\Administrator\Desktop\test.py", line 346, in <module>
    print (fact(1000))
  File "C:\Users\Administrator\Desktop\test.py", line 345, in fact
    return n * fact(n - 1)
  File "C:\Users\Administrator\Desktop\test.py", line 345, in fact
    return n * fact(n - 1)
  File "C:\Users\Administrator\Desktop\test.py", line 345, in fact
    return n * fact(n - 1)
  [Previous line repeated 994 more times]
  File "C:\Users\Administrator\Desktop\test.py", line 343, in fact
    if n==1:
RecursionError: maximum recursion depth exceeded in comparison
```

解决：

fact\(5\)对应的fact\_iter\(5, 1\)的调用如下：

```
===> fact_iter(5, 1)
===> fact_iter(4, 5)
===> fact_iter(3, 20)
===> fact_iter(2, 60)
===> fact_iter(1, 120)
===> 120
```





