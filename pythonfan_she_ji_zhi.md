# Python反射机制

　　对编程语言比较熟悉的朋友，应该知道“反射”这个机制。Python作为一门动态语言，当然不会缺少这一重要功能。然而，在网络上却很少见到有详细或者深刻的剖析论文。下面结合一个web路由的实例来阐述python的反射机制的使用场景和核心本质。
  
  
##一、web实例

  考虑有这么一个场景，根据用户输入的url的不同，调用不同的函数，实现不同的操作，也就是一个url路由器的功能，这在web框架里是核心部件之一。下面有一个精简版的示例：


<pre>

#首先，有一个commons模块，它里面有几个函数，分别用于展示不同的页面，代码如下：
 
def login():
    print("这是一个登陆页面！")
 
 
def logout():
    print("这是一个退出页面！")
 
 
def home():
    print("这是网站主页面！")
    
    
 #其次，有一个visit模块，作为程序入口，接受用户输入，展示相应的页面，代码如下：（这段代码是比较初级的写法）
 
 
 import commons
 
 
def run():
    inp = input("请输入您想访问页面的url：  ").strip()
    if inp == "login":
        commons.login()
    elif inp == "logout":
        commons.logout()
    elif inp == "home":
        commons.home()
    else:
        print("404")
 
 
if __name__ == '__main__':
    run()
 
 
#我们运行visit.py，输入：home，页面结果如下：
请输入您想访问页面的url：  home
这是网站主页面！
 
 
</pre>

　这就实现了一个简单的WEB路由功能，根据不同的url，执行不同的函数，获得不同的页面。

　　然而，让我们考虑一个问题，如果commons模块里有成百上千个函数呢(这非常正常)?。难道你在visit模块里写上成百上千个elif?显然这是不可能的！那么怎么破？
  
##二、反射机制

仔细观察visit中的代码，我们会发现用户输入的url字符串和相应调用的函数名好像！如果能用这个字符串直接调用函数就好了！但是，前面我们已经说了字符串是不能用来调用函数的。为了解决这个问题，python为我们提供一个强大的内置函数：getattr!我们将前面的visit修改一下，代码如下：

<pre>
#注意： 如果页面处理函数往往被分类放置在不同目录的不同模块中，例如上千个函数与模块，这样如果要实现上面的实例，需要很多import语句导入上百个模块， visit模块要对访问的url上千个判断，是否很累。

　#实现
 #python提供了一个特殊的方法：__import__(字符串参数)。通过它，我们就可以实现类似的反射功能。__import__()方法会根据参数，动态的导入同名的模块。

def run():
    inp = input("请输入您想访问页面的url：  ").strip()
    modules, func = inp.split("/")
    obj = __import__(modules)
    if hasattr(obj, func):
        func = getattr(obj, func)
        func()
    else:
        print("404")
 
if __name__ == '__main__':
    run()


#如果模块不在一个目录的情况：

def run():
    inp = input("请输入您想访问页面的url：  ").strip()
    modules, func = inp.split("/")
    obj = __import__("lib." + modules, fromlist=True)  # 注意fromlist参数
    if hasattr(obj, func):
        func = getattr(obj, func)
        func()
    else:
        print("404")
 
if __name__ == '__main__':
    run()

</pre>
