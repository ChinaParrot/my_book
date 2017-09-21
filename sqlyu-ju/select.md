SELECT 语句的基本格式为：

```
USE db; #进入要执行的库
SELECT 要查询的列名 FROM 表名字 WHERE 限制条件;
```

* 查询列名： 可以指定具体列名；如果使用'\*'代表要查询表中所有的列。
* 限制条件：

 1、WHERE限制条件可以有数学符号 \(=,&lt;,&gt;,&gt;=,&lt;=\)，字段添加条件实现更精准的查询。

```
SELECT name,age FROM employee WHERE age>25;
SELECT name,age,phone FROM employee WHERE name='Mary';
```

2、使用多个条件，可以使用OR\(或\) 和 AND\(且\) 连接。

```
SELECT name,age FROM employee WHERE age<25 OR age>30;
```



