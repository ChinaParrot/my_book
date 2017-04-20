#  linux的find命令详解
find命令是用来在给定的目录下查找符合给定条件的文件

## 查找条件
**1、根据名称查找**

　-name "PATERN"
　-iname "PATERN"： 不区分名称字母大小写
  -regex "PATTERN"：基于正则表达式的模式查找，匹配的是整个路径，而非单个文件名。


**2、根据文件从属关系查找**

-user USERNAME：查找属主指定用户的所有文件；
-group GRPNAME：查找属组指定组的所有文件； 
-uid UID：查找属主指定的UID的所有文件；
-gid GID：查找属组指定的GID的所有文件；


 