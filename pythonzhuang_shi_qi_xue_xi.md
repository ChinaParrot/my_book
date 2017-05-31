# Python装饰器学习

装饰器本质上是一个函数，该函数用来处理其他函数，它可以让其他函数在不需要修改代码的前提下增加额外的功能，装饰器的返回值也是一个函数对象。它经常用于有切面需求的场景，比如：插入日志、性能测试、事务处理、缓存、权限校验等应用场景。装饰器是解决这类问题的绝佳设计，有了装饰器，我们就可以抽离出大量与函数功能本身无关的雷同代码并继续重用。概括的讲，装饰器的作用就是为已经存在的对象添加额外的功能。

```
def outer(fun):
def wrapper(arg):
    print ('添加验证')
fun(arg)
    print ('test')
    return (wrapper)
@outer
def Funct1(arg):
    print ('func1',arg)
@outer = outer(Funct1)
@outer
def Funct2():
    print ('func2')
Funct1(test)
Funct2()

```

Python中有一个被称为属性函数\(property\)的小概念，它可以做一些有用的事情。在这篇文章中，我们将看到如何能做以下几点：

将类方法转换为只读属性

重新实现一个属性的setter和getter方法

在本文中，您将学习如何以几种不同的方式来使用内置的属性函数。希望读到文章的末尾时，你能看到它是多么有用。

开始

使用属性函数的最简单的方法之一是将它作为一个方法的装饰器来使用。这可以让你将一个类方法转变成一个类属性。当我需要做某些值的合并时，我发现这很有用。其他想要获取它作为方法使用的人，发现在写转换函数时它很有用。让我们来看一个简单的例子：



```
########################################################################
class Person(object):
""""""

#----------------------------------------------------------------------
def __init__(self, first_name, last_name):
"""Constructor"""
self.first_name = first_name
self.last_name = last_name

#----------------------------------------------------------------------
@property
def full_name(self):
"""
Return the full name
"""
return "%s %s" % (self.first_name, self.last_name)
########################################################################
class Person(object):
""""""
#----------------------------------------------------------------------
def __init__(self, first_name, last_name):
"""Constructor"""
self.first_name = first_name
self.last_name = last_name
#----------------------------------------------------------------------
@property
def full_name(self):
"""
Return the full name
"""
return "%s %s" % (self.first_name, self.last_name)
```

在上面的代码中，我们创建了两个类属性：self.first\_name和self.last\_name。接下来，我们创建了一个full\_name方法，它有一个@property装饰器。这使我们能够在Python解释器会话中有如下的交互：

```
>>> person = Person("Mike", "Driscoll")
>>> person.full_name
'Mike Driscoll'
>>> person.first_name
'Mike'
>>> person.full_name = "Jackalope"
Traceback (most recent call last):
File "<string>", line 1, in <fragment>
AttributeError: can't set attribute
>>> person = Person("Mike", "Driscoll")
>>> person.full_name
'Mike Driscoll'
>>> person.first_name
'Mike'
>>> person.full_name = "Jackalope"
Traceback (most recent call last):
File "<string>", line 1, in <fragment>
AttributeError: can't set attribute
```

正如你所看到的，因为我们将方法变成了属性，我们可以使用正常的点符号访问它。但是，如果我们试图将该属性设为其他值，我们会引发一个AttributeError错误。改变full\_name属性的唯一方法是间接这样做：



