[CSV \(Comma Separated Values\)](http://zh.wikipedia.org/zh-cn/逗号分隔值)，即逗号分隔值（也称字符分隔值，因为分隔符可以不是逗号），是一种常用的文本

格式，用以存储表格数据，包括数字或者字符。很多程序在处理数据时都会碰到csv这种格式的文件，它的使用是比

较广泛的（Kaggle上一些题目提供的数据就是csv格式），csv虽然使用广泛，但却没有通用的标准，所以在处理csv

格式时常常会碰到麻烦，幸好python内置了csv模块。下面简单介绍csv模块中最常用的一些函数。

```
reader(csvfile, dialect='excel', **fmtparams)
参数说明：

csvfile，必须是支持迭代(Iterator)的对象，可以是文件(file)对象或者列表(list)对象，如果是文件对
象，打开时需要加"b"标志参数。

dialect，编码风格，默认为excel的风格，也就是用逗号（,）分隔，dialect方式也支持自定义，通过调用register_dialect方法来注册，下文会提到。

fmtparam，格式化参数，用来覆盖之前dialect对象指定的编码风格。
```

```
import csv  
with open('test.csv','rb') as myFile:  
    lines=csv.reader(myFile)  
    for line in lines:  
        print line  
```



