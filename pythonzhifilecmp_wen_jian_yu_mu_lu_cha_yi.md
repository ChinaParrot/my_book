# Python之filecmp文件与目录差异

当我们进行代码审计或校验备份结果时，往往需要检查原始与目标目录的文件一致性，Python的标准库已经自带了满足此需求的模块filecmp。filecmp可以实现文件、目录、遍历子目录的差异对比功能。比如报告中输出目标目录比原始多出的文件或子目录，即使文件同名也会判断是否为同一个文件（内容级对比）等，Python 2.3或更高版本默认自带filecmp模块，无需额外安装。

filecmp提供了三个操作方法，分别为cmp（单文件对比）、cmpfiles（多文件对比）、dircmp（目录对比）

##cmp（单文件对比）
单文件对比，采用filecmp.cmp(f1, f2[, shallow])方法，比较文件名为f1和f2的文件，相同返回True，不相同返回False，shallow默认为True，意思是只根据os.stat()方法返回的文件基本信息进行对比，比如最后访问时间、修改时间、状态改变时间等，会忽略文件内容的对比。当shallow为False时，则os.stat()与文件内容同时进行校验。

示例：比较单文件的差异。

```
>>> filecmp.cmp("/home/test/filecmp/f1","/home/test/filecmp/f3")
True
>>> filecmp.cmp("/home/test/filecmp/f1","/home/test/filecmp/f2")
False

```
##cmpfiles（多文件对比）
