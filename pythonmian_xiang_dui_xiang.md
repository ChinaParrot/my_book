# python面向对象

面向对象编程——Object Oriented Programming，简称OOP，是一种程序设计思想。OOP把对象作为程序的基本单元，一个对象包含了数据和操作数据的函数。

**面向对象技术简介**

1. \(Class\): 用来描述具有相同的属性和方法的对象的集合。它定义了该集合中每个对象所共有的属性和方法。对象是类的实例。
2. 类变量：类变量在整个实例化的对象中是公用的。类变量定义在类中且在函数体之外。类变量通常不作为实例变量使用。
3. 数据成员：类变量或者实例变量用于处理类及其实例对象的相关的数据。
4. 方法重写：如果从父类继承的方法不能满足子类的需求，可以对其进行改写，这个过程叫方法的覆盖（override），也称为方法的重写。
5. 实例变量：定义在方法中的变量，只作用于当前实例的类。
6. 继承：即一个派生类（derived class）继承基类（base class）的字段和方法。继承也允许把一个派生类的对象作为一个基类对象对待。例如，有这样一个设计：一个Dog类型的对象派生自Animal类，这是模拟"是一个（is-a）"关系（例图，Dog是一个Animal）。
7. 实例化：创建一个类的实例，类的具体对象。
8. 方法：类中定义的函数。
9. 对象：通过类定义的数据结构实例。对象包括两个数据成员（类变量和实例变量）和方法。

**创建类**

使用class语句来创建一个新类，class之后为类的名称并以冒号结尾，如下实例:

```
class ClassName:
    '类的帮助信息' #类文档字符串
    class_suite #类体
```

实例：

如果采用面向对象的程序设计思想，我们首选思考的不是程序的执行流程，而是Student这种数据类型应该被视为一个对象，这个对象拥有name和score这两个属性（Property）。如果要打印一个学生的成绩，首先必须创建出这个学生对应的对象，然后，给对象发一个print\_score消息，让对象自己把自己的数据打印出来。

```
#!/usr/bin/env python3
# -*- coding: UTF-8 -*-
class Student(object):
    #静态字段
    test01 = 'test'
    def __init__(self, name, score):
    #动态字段
        self.name = name
        self.score = score

    def print_score(self):
        print ('%s: %s' % (self.name, self.score))
#调用
lisi = Student('lisi',12)
zhangsan = Student('zhangsan',13)
lisi.print_score()
zhangsan.print_score()
print (Student.test01)
```

注意到\_\_init\_\_方法的第一个参数永远是self，表示创建的实例本身，因此，在\_\_init\_\_方法内部，就可以把各种属性绑定到self，因为self就指向创建的实例本身。

有了\_\_init\_\_方法，在创建实例的时候，就不能传入空的参数了，必须传入与\_\_init\_\_方法匹配的参数，但self不需要传，Python解释器自己会把实例变量传进去。

和普通的函数相比，在类中定义的函数只有一点不同，就是第一个参数永远是实例变量self，并且，调用时，不用传递该参数。除此之外，类的方法和普通函数没有什么区别，所以，你仍然可以用默认参数、可变参数和关键字参数。

**私有变量                              
**

如果要让内部属性不被外部访问，可以把属性的名称前加上两个下划线\_\_，在Python中，实例的变量名如果以\_\_开头，就变成了一个私有变量（private），只有内部可以访问，外部不能访问。

```
#!/usr/bin/env python3
# -*- coding: UTF-8 -*-
class Student(object):
    def __init__(self, name, score):
        self.__name = name
        self.__score = score
    def print_score(self):
        print ('%s: %s' % (self.__name, self.__score))
```

改完后，对于外部代码来说，没什么变动，但是已经无法从外部访问实例变量.\_\_name和实例变量.\_\_score了：

```
>>> bart = Student('Bart Simpson', 98)
>>> bart.__name
Traceback (most recent call last):
File "<stdin>", line 1, in <module>
AttributeError: 'Student' object has no attribute '__name'
```

这样就确保了外部代码不能随意修改对象内部的状态，这样通过访问限制的保护，代码更加健壮。

但是如果外部代码要获取name和score怎么办？可以给Student类增加get\_name和get\_score这样的方法：

```
#!/usr/bin/env python3
# -*- coding: UTF-8 -*-
class Student(object):
    def __init__(self, name, score):
        self.__name = name
        self.__score = score
    def print_score(self):
        print ('%s: %s' % (self.__name, self.__score))
    def get_name(self):
        return self.__name

    def get_score(self):
        return self.__score

#调用
zhangsan = Student('zhangsan',13)
print (zhangsan.get_name())
print (zhangsan.get_score())
```

如果又要允许外部代码修改score怎么办？可以给Student类增加set\_score方法：

```
class Student(object):
...

    def set_score(self, score):
        self.__score = score
```

Python不允许实例化的类访问私有数据，但你可以使用 \#object.\_className\_\_attrName 访问属性：

```
#!/usr/bin/env python3
# -*- coding: UTF-8 -*-

class JustCounter:
    __secretCount = 0 # 私有变量
    publicCount = 0 # 公开变量

    def count(self):
        self.__secretCount += 1
        self.publicCount += 1
        print (self.__secretCount)
counter = JustCounter()
counter.count()
counter.count()
print (counter.publicCount)
print (counter.__secretCount) # 报错，实例不能访问私有变量
print (counter._JustCounter__secretCount)
```

你也可以使用以下函数的方式来访问属性：

1. getattr\(obj, name\[, default\]\) : 访问对象的属性。  
2. hasattr\(obj,name\) : 检查是否存在一个属性。  
3. setattr\(obj,name,value\) : 设置一个属性。如果属性不存在，会创建一个新属性。  
4. delattr\(obj, name\) : 删除属性。

**Python内置类属性**

1. \_\_dict\_\_ : 类的属性（包含一个字典，由类的数据属性组成）

2. \_\_doc\_\_ :类的文档字符串

3. \_\_name\_\_: 类名

4. \_\_module\_\_: 类定义所在的模块（类的全名是'\_\_main\_\_.className'，如果类位于一个导入模块mymod中，那么className.\_\_module\_\_ 等于 mymod）

5. \_\_bases\_\_ : 类的所有父类构成元素（包含了以个由所有父类组成的元组）

```
#!/usr/bin/env python3
#-*- coding: UTF-8 -*-
class Student(object):
    '学生基本信息的基类'
    def __init__(self,name,score):
        self.__name = name
        self.__score = score
    def print_score(self):
        print ('%s: %s' %(self.get_name(),self.get_score()))
    def get_name(self):
        return self.__name
    def get_score(self):
        return self.__score

lisi = Student('lisi',12)
zhansan = Student('zhangsan',13)

print ("Student.__doc__: ",Student.__doc__)
print  ("Student.__name__:",Student.__name__)
print ("Student.__bases__:",Student.__bases__)
print ("Student.__dict__:",Student.__dict__)
```

**类的继承**

面向对象的编程带来的主要好处之一是代码的重用，实现这种重用的方法之一是通过继承机制。继承完全可以理解成类之间的类型和子类型关系。

需要注意的地方：继承语法 class 派生类名（基类名）：//... 基类名写作括号里，基本类是在类定义的时候，在元组之中指明的。

在python中继承中的一些特点：

1. 在继承中基类的构造（\_\_init\_\_\(\)方法）不会被自动调用，它需要在其派生类的构造中亲自专门调用。

2. 在调用基类的方法时，需要加上基类的类名前缀，且需要带上self参数变量。区别于在类中调用普通函数时并不需要带上self参数

3. Python总是首先查找对应类型的方法，如果它不能在派生类中找到对应的方法，它才开始到基类中逐个查找。（先在本类中查找调用的方法，找不到才去基类中找）。

如果在继承元组中列了一个以上的类，那么它就被称作"多重继承" 。

```
#!/usr/bin/env python3
# -*- coding: UTF-8 -*-

class Parent:        # 定义父类
   parentAttr = 100
   def __init__(self):
      print ("调用父类构造函数")

   def parentMethod(self):
      print ('调用父类方法')

   def setAttr(self, attr):
      Parent.parentAttr = attr

   def getAttr(self):
      print ("父类属性 :", Parent.parentAttr)

class Child(Parent): # 定义子类
   def __init__(self):
      print ("调用子类构造方法")

   def childMethod(self):
      print ('调用子类方法 child method')
c = Child() # 实例化子类
c.childMethod() # 调用子类的方法
c.parentMethod() # 调用父类方法
c.setAttr(200) # 再次调用父类的方法
c.getAttr() # 再次调用父类的方法


#结果
调用子类构造方法
调用子类方法 child method
调用父类方法
父类属性 : 200
```

**方法重写**

如果你的父类方法的功能不能满足你的需求，你可以在子类重写你父类的方法：

```
#!/usr/bin/env python3
# -*- coding: UTF-8 -*-

class Parent: # 定义父类
    def myMethod(self):
        print ('调用父类方法')

class Child(Parent): # 定义子类
    def myMethod(self):
        print ('调用子类方法')

c = Child() # 子类实例
c.myMethod() # 子类调用重写方法

#执行以上代码输出结果如下：
调用子类方法

```

**静态变量与私有**

```
#!/usr/bin/env python3
#-*- coding:utf-8 -*-

class MsqlHelper:
    def add(self,sql):
        pass
    def delete(self,sql):
        pass
    def update(self,sql):
        pass
    def select(self,sql):
        pass

sql = 'test'
#如果多个业务需要创建多个对象，开辟多个内存空间，解决使用静态。
ms = MsqlHelper()
ms.update(sql)

class MsqlHelper02:
    @staticmethod
    def add(sql):
        pass
    @staticmethod
    def delete(sql):
        pass
    @staticmethod
    def update(sql):
        pass
    @staticmethod
    def select(sql):
        pass
MsqlHelper02.update(sql)

```

析构函数和特殊的\_\_call\_\_方法

```
import time
class Foo:
    def __init__(self):
        pass
    def __del__(self):
        print ('解释器要销毁我了，我要做租后一次的呐喊！')
    def Go(self):
        print ('GO')
    def __call__(self):
        print ('call')
#f1 = Foo() #实例化类
#f1.Go()

#time.sleep(100)

#f1() #执行类的 __call__ 方法；实例化对象

Foo()
f1 = Foo()
f1()

```



