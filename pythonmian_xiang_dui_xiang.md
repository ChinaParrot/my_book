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



