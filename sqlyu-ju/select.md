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

2、使用多个条件，可以使用OR\(或\) 和 AND\(且\) 连接。

```
SELECT name,age FROM employee WHERE age<25 OR age>30;

#格式
SELECT name,age FROM employee WHERE age>25 and age>30;

SELECT name,age FROM employee WHERE age BETWEEN 25 AND 30
```

3、在某个范围使用IN 和 NOT IN

```
SELECT name,age,phone,in_dpt FROM employee WHERE in_dpt IN ('dpt3','dpt4');
SELECT name,age,phone,in_dpt FROM employee WHERE in_dpt NOT IN ('dpt3','dpt4');
```

4、关键字 LIKE 在SQL语句中和通配符一起使用，通配符代表未知字符。SQL中的通配符是 \_ 和 % 。其中 \_ 代表一个未指定字符，% 代表不定个未指定字符。

```
SELECT name,age,phone FROM employee WHERE phone LIKE '1101__';
SELECT name,age,phone FROM employee WHERE phone LIKE '1101%';
```

5、结果排序

为了使查询结果看起来更顺眼，我们可能需要对结果按某一列来排序，这就要用到 ORDER BY 排序关键词。默认情况下，ORDER BY的结果是升序排列，而使用关键词ASC和DESC可指定升序或降序排序。 比如，我们按salary降序排列，SQL语句为：

```
SELECT name,age,salary,phone FROM employee ORDER BY salary DESC;
```

6、mysql内置函数

| 函数名 | COUNT | SUM | AVG | MAX | MIN |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 作用 | 计数 | 求和 | 求平均值 | 最大值 | 最小值 |

```
SELECT MAX(salary) AS max_salary,MIN(salary) FROM employee;
```

7、子查询

一般SELECT 语句都仅涉及一个表中的数据，然而有时必须处理多个表才能获得所需的信息，子查询还可以扩展到3层、4层或更多层。

```
SELECT
	of_dpt,
	COUNT(proj_name) AS count_project
FROM
	project
WHERE
	of_dpt IN (
		SELECT
			in_dpt
		FROM
			employee
		WHERE
			NAME = 'Tom'
	);
```



