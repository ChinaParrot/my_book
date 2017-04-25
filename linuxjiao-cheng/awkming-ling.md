awk是一种编程语言，用于在linux/unix下对文本和数据进行处理。数据可以来自标准输入\(stdin\)、一个或多个文件，或其它命令的输出。它支持用户自定义函数和动态正则表达式等先进功能，是linux/unix下的一个强大编程工具。它在命令行中使用，但更多是作为脚本来使用。awk有很多内建的功能，比如数组、函数等，这是它和C语言的相同之处，灵活性是awk最大的优势。

# **一、常用命令选项**

```
-F fs   fs指定输入分隔符，fs可以是字符串或正则表达式，如-F: 
-v var=value   赋值一个用户定义变量，将外部变量传递给awk 
-f scripfile  从脚本文件中读取awk命令 
-m[fr] val   对val值设置内在限制，-mf选项限制分配给val的最大块数目；-mr选项限制记录的最大数目。这两个功能是Bell实验室版awk的扩展功能，在标准awk中不适用。
```

# 二、awk模式和操作

1. 模式可以是以下任意一个： 

/正则表达式/：使用通配符的扩展集。

关系表达式：使用运算符进行操作，可以是字符串或数字的比较测试。

模式匹配表达式：用运算符~（匹配）和~!（不匹配）。

```
//纯字符匹配   !//纯字符不匹配   
~//字段值匹配    !~//字段值不匹配   ~/a1|a2/字段值匹配a1或a2
```

BEGIN语句块、pattern语句块、END语句块。

1. 操作由一个或多个命令、函数、表达式组成，之间由换行符或分号隔开，并位于大括号内，主要部分是：

变量或数组赋值

输出命令

内置函数

控制流语句

# 三、awk脚本基本结构

`awk 'BEGIN{ print "start" } pattern{ commands } END{ print "end" }' file`

一个awk脚本通常由：BEGIN语句块、能够使用模式匹配的通用语句块、END语句块3部分组成，这三个部分是可选的。任意一个部分都可以不出现在脚本中，脚本通常是被单引号或双引号中，例如：

```
awk "BEGIN{ i=0 } { i++ } END{ print i }" filename
awk 'BEGIN{ i=0 } { i++ } END{ print i }' filename
```

**工作原理：**

```
第一步：执行BEGIN{ commands }语句块中的语句；
第二步：从文件或标准输入(stdin)读取一行，然后执行pattern{ commands }语句块，它逐行扫描文件，从第一行到最后一行重复这个过程，直到文件全部被读取完毕。 
第三步：当读至输入流末尾时，执行END{ commands }语句块。 BEGIN语句块在awk开始从输入流中读取行之前被执行，这是一个可选的语句块，比如变量初始化、打印输出表格的表头等语句通常可以写在BEGIN语句块中。 END语句块在awk从输入流中读取完所有的行之后即被执行，比如打印所有行的分析结果这类信息汇总都是在END语句块中完成，它也是一个可选语句块。 pattern语句块中的通用命令是最重要的部分，它也是可选的。如果没有提供pattern语句块，则默认执行{ print }，即打印每一个读取到的行，awk读取的每一行都会执行该语句块。
```

# 三、awk内置变量（预定义变量）

| **属性** | **说明** |
| :--- | :--- |
| $0 | 当前记录（作为单个变量） |
| $1~$n | 当前记录的第n个字段，字段间由FS分隔 |
| FS | 输入字段分隔符 默认是空格 |
| NF | 当前记录中的字段个数，就是有多少列 |
| NR | 已经读出的记录数，就是行号，从1开始 |
| RS | 输入的记录他隔符默 认为换行符 |
| OFS | 输出字段分隔符 默认也是空格 |
| ORS | 输出的记录分隔符，默认为换行符 |
| ARGC | 命令行参数个数 |
| ARGV | 命令行参数数组 |
| FILENAME | 当前输入文件的名字 |
| IGNORECASE | 如果为真，则进行忽略大小写的匹配 |
| ARGIND | 当前被处理文件的ARGV标志符 |
| CONVFMT | 数字转换格式 %.6g |
| ENVIRON | UNIX环境变量 |
| ERRNO | UNIX系统错误消息 |
| FIELDWIDTHS | 输入字段宽度的空白分隔字符串 |
| FNR | 当前记录数 |
| OFMT | 数字的输出格式 %.6g |
| RSTART | 被匹配函数匹配的字符串首 |
| RLENGTH | 被匹配函数匹配的字符串长度 |
| SUBSEP | \034 |

**例子：**

```
#/^root/ 为选择表达式，$0代表是逐行
awk '/^root/{print $0}' /etc/passwd 

#设置字段分隔符号(FS使用方法）
awk 'BEGIN{FS=":"}/^root/{print $1,$NF}' /etc/passwd

#记录条数(NR,FNR使用方法)
awk 'BEGIN{FS=":"}{print NR,$1,$NF}' /etc/passwd

#设置输出字段分隔符（OFS使用方法) 
 awk 'BEGIN{FS=":";OFS="^^"}/^root/{print FNR,$1,$NF}' /etc/passwd

#设置输出行记录分隔符(ORS使用方法）
awk 'BEGIN{FS=":";ORS="^^"}{print FNR,$1,$NF}' /etc/passwd

#输入参数获取(ARGC ,ARGV使用）
awk 'BEGIN{FS=":";print "ARGC="ARGC;for(k in ARGV) {print k"="ARGV[k]; }}' /etc/passwd

#获得传入的文件名(FILENAME使用)
awk 'BEGIN{FS=":";print FILENAME}{print FILENAME}' /etc/passwd 
FILENAME,$0-$N,NF 不能使用在BEGIN中，BEGIN中不能获得任何与文件记录操作的变量。

#获得linux环境变量（ENVIRON使用）
awk 'BEGIN{print ENVIRON["PATH"];}' /etc/passwd 

#输出数据格式设置：(OFMT使用） 
awk 'BEGIN{OFMT="%.3f";print 2/3,123.11111111;}' /etc/passwd 
0.667 123.111
```

# 三、awk运算与判断

作为一种程序设计语言所应具有的特点之一，awk支持多种运算，这些运算与C语言提供的基本相同。awk还提供了一系列内置的运算函数（如log、sqr、cos、sin等）和一些用于对字符串进行操作（运算）的函数（如length、substr等等）。这些函数的引用大大的提高了awk的运算功能。作为对条件转移指令的一部分，关系判断是每种程序设计语言都具备的功能，awk也不例外，awk中允许进行多种测试，作为样式匹配，还提供了模式匹配表达式~（匹配）和~!（不匹配）。作为对测试的一种扩充，awk也支持用逻辑运算符。

| 运算符 | 描述 |
| :--- | :--- |
| + - | 加，减 |
| \* / & | 乘，除与求余 |
| + - ! | 一元加，减和逻辑非 |
| ^ \*\*\* | 求幂 |
| ++ -- | 增加或减少，作为前缀或后缀 |
| = += -= \*= /= %= ^= \*\*= | 赋值语句 |
| \|\| | 逻辑或 |
| && | 逻辑与 |
| ~ ~! | 匹配正则表达式和不匹配正则表达式 |
| &lt; &lt;= &gt; &gt;= != == | 关系运算符 |
|  |  |

# 三、awk高级输入输出

```
cat text.txt
 a
 b
 c
 d 
 e 
 
awk 'NR%2==1{next}{print NR,$0;}' text.txt 
2 b 
4 d

```

当记录行号除以2余1，就跳过当前行。下面的print NR,$0也不会执行。下一行开始，程序有开始判断NR%2值。这个时候记录行号是：2 ，就会执行下面语句块：'print NR,$0'

# 四、流程控制语句

```
#统计某个文件夹下的文件占用的字节数,过滤4096大小的文件(一般都是文件夹)
ls -l |awk 'BEGIN {size=0;print "[start]size is ", size} {if($5!=4096){size=size+$5;}} END{print "[end]size is ", size/1024/1024,"M"}' 
```



