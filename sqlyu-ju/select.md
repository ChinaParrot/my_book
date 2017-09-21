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

也可以是正则：

使用REGEXP关键字来指定正则表达式

![](/assets/正则.png)

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

8、连接查询

在处理多个表时，子查询只有在结果来自一个表时才有用。但如果需要显示两个表或多个表中的数据，这时就必须使用连接 \(join\) 操作。 连接的基本思想是把两个或多个表当作一个新的表来操作，如下：

```
SELECT id,name,people_num
FROM employee,department
WHERE employee.in_dpt = department.dpt_name ORDER BY id;

SELECT a.id,a.name,a.people_num,b.id,b.name,b.people_num
FROM employee AS a,department AS b
WHERE a.in_dpt = b.dpt_name ORDER BY id;
```

* 内连接

内连接是将符合查询条件\(符合连接条件\)的行返回，也就是相关联的行就返回。

* ```
  SELECT id,name,people_num FROM employee JOIN department ON employee.in_dpt = department.dpt_name ORDER BY id;

  SELECT id,name,people_num FROM employee INNER JOIN department ON employee.in_dpt = department.dpt_name ORDER BY id;
  ```
* 外连接

外连接除了返回相关联的行之外，将没有关联的行也会显示出来。

**左外连接：**

格式：表名 LEFT JOIN 表名 ON 条件；

返回包括左表中的所有记录和右表中连接字段相等的记录，通俗点讲，就是除了显示相关联的行，还会将左表中的所有记录行度显示出来，右边没有的部分null显示。

```
SELECT id,name,people_num FROM employee AS e LEFT JOIN department AS d ON e.in_dpt = d.dpt_name;
```

**右外连接：**

格式： 表名 RIGHT JOIN 表名 ON 条件

返回包括右表中的所有记录和右表中连接字段相等的记录。其实跟左外连接差不多，就是将右边的表给全部显示出来

```
SELECT id,name,people_num FROM employee AS e RIGHT JOIN department AS d ON e.in_dpt = d.dpt_name;
```



