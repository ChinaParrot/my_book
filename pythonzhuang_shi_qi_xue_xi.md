# Python装饰器学习

装饰器本质上是一个函数，该函数用来处理其他函数，它可以让其他函数在不需要修改代码的前提下增加额外的功能，装饰器的返回值也是一个函数对象。它经常用于有切面需求的场景，比如：插入日志、性能测试、事务处理、缓存、权限校验等应用场景。装饰器是解决这类问题的绝佳设计，有了装饰器，我们就可以抽离出大量与函数功能本身无关的雷同代码并继续重用。概括的讲，装饰器的作用就是为已经存在的对象添加额外的功能。

例如：

<pre>
def outer(fun):
    def wrapper(arg):
      print '添加验证'
      fun(arg)
      print 'test'
     return wrapper
     
 @outer 
 def Funct1(arg):
   print 'func1',arg
   
@outer = outer(Funct1)
   
 @outer
 def Funct2():
   print 'func2'

Funct1(test)
Funct2()

</pre>