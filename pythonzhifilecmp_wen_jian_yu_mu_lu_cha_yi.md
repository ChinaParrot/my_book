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
多文件对比，采用filecmp.cmpfiles(dir1, dir2, common[, shallow])方法，对比dir1与dir2目录给定的文件清单。该方法返回文件名的三个列表，分别为匹配、不匹配、错误。匹配为包含匹配的文件的列表，不匹配反之，错误列表包括了目录不存在文件、不具备读权限或其他原因导致的不能比较的文件清单。

示例：dir1与dir2目录中指定文件清单对比。

```
两目录下文件的md5信息如下，其中f1、f2文件匹配；f3不匹配；f4、f5对应目录中不存在，无法比较。
[root@SN2013-08-020 dir2]# md5sum *        
d9dfc198c249bb4ac341198a752b9458  f1
aa9aa0cac0ffc655ce9232e720bf1b9f  f2
33d2119b71f717ef4b981e9364530a39  f3
d9dfc198c249bb4ac341198a752b9458  f5
 [root@SN2013-08-020 dir1]# md5sum *  
d9dfc198c249bb4ac341198a752b9458  f1
aa9aa0cac0ffc655ce9232e720bf1b9f  f2
d9dfc198c249bb4ac341198a752b9458  f3
410d6a485bcf5d2d2d223f2ada9b9c52  f4
使用cmpfiles对比的结果如下，符合我们的预期。

>>>filecmp.cmpfiles("/home/test/filecmp/dir1","/home/test/filecmp/dir2",['f1','f2','f3','f4','f5'])

(['f1', 'f2'], ['f3'], ['f4', 'f5'])

目录对比，通过dircmp(a, b[, ignore[, hide]])类创建一个目录比较对象，其中a和b是参加比较的目录名。ignore代表文件名忽略的列表，并默认为['RCS', 'CVS', 'tags']；hide代表隐藏的列表，默认为[os.curdir，os.pardir]。dircmp类可以获得目录比较的详细信息，如只有在a目录中包括的文件、a与b都存在的子目录、匹配的文件等，同时支持递归。
```

##dircmp（目录对比）
dircmp提供了三个输出报告的方法：

* report()，比较当前指定目录中的内容；
* report_partial_closure()，比较当前指定目录及第一级子目录中的内容；
* report_full_closure()，递归比较所有指定目录的内容。

为输出更加详细的比较结果，dircmp类还提供了以下属性：

* left，左目录，如类定义中的a；
* right，右目录，如类定义中的b；
* left_list，左目录中的文件及目录列表；
* right_list，右目录中的文件及目录列表；
* common，两边目录共同存在的文件或目录；
* left_only，只在左目录中的文件或目录；
* right_only，只在右目录中的文件或目录；
* common_dirs，两边目录都存在的子目录；
* common_files，两边目录都存在的子文件；
* common_funny，两边目录都存在的子目录（不同目录类型或os.stat()记录的错误）；
* same_files，匹配相同的文件；
* diff_files，不匹配的文件；
* funny_files，两边目录中都存在，但无法比较的文件；
* subdirs，将common_dirs目录名映射到新的dircmp对象，格式为字典类型。


