#  linux的find命令详解
find命令是用来在给定的目录下查找符合给定条件的文件

## 查找条件
**1、根据名称查找**

　-name "PATERN"
　-iname "PATERN"： 不区分名称字母大小写
  -regex PATTERN：基于正则表达式的模式查找，匹配的是整个路径，而非单个文件名。


**2、**