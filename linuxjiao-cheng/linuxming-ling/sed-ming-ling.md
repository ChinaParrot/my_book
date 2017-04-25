sed是一种流编辑器，它是文本处理中非常中的工具，能够完美的配合正则表达式使用，功能不同凡响。处理时，把当前处理的行存储在临时缓冲区中，称为“模式空间”（pattern space），接着用sed命令处理缓冲区中的内容，处理完成后，把缓冲区的内容送往屏幕。接着处理下一行，这样不断重复，直到文件末尾。文件内容并没有 改变，除非你使用重定向存储输出。Sed主要用来自动编辑一个或多个文件；简化对文件的反复操作；编写转换程序等。

# 一、命令参数

| 参数 | 详解 |
| :--- | :--- |
| **a\** | 在当前行下面插入文本。 |
| **i\** | 在当前行上面插入文本。 |
| **c ** | 把选定的行改为新的文本。 |
| ** d ** | 删除，删除选择的行。 |
| **D** | 删除模板块的第一行。 |
| ** s** | 替换指定字符 |
| **h** | 拷贝模板块的内容到内存中的缓冲区。 |
| ** H** | 追加模板块的内容到内存中的缓冲区。 |
| ** g** | 获得内存缓冲区的内容，并替代当前模板块中的文本。 |
| ** G ** | 获得内存缓冲区的内容，并追加到当前模板块文本的后面。 |
| ** l** | 列表不能打印字符的清单。 |
| **n** | 读取下一个输入行，用下一个命令处理新的行而不是用第一个命令。 |
| **N** | 追加下一个输入行到模板块后面并在二者间嵌入一个新行，改变当前行号码。 |
| **p** | 打印模板块的行。 |
| **P** | 打印模板块的第一行。 |
| **q** | 退出Sed |
| **b** | lable 分支到脚本中带有标记的地方，如果分支不存在则分支到脚本的末尾。 |
| **r** | file 从file中读行。 |
| **t** | label if分支，从最后一行开始，条件一旦满足或者T，t命令，将导致分支到带有标号的命令处，或者到脚本的末尾。 |
| **T** | label 错误分支，从最后一行开始，一旦发生错误或者T，t命令，将导致分支到带有标号的命令处，或者到脚本的末尾。 |
| **w** | file 写并追加模板块到file末尾。 |
| **W** | file 写并追加模板块的第一行到file末尾。 |
| **!** | 表示后面的命令对所有没有被选定的行发生作用。 |
| **=** | 打印当前行号码。 |
| **\#** | 把注释扩展到下一个换行符以前。 |
| **f** | 直接将 sed 的动作写在一个文件内， -f filename 则可以运行 filename 内的 sed 动作； |

```
#sed元字符集 


^ 匹配行开始，如：/^sed/匹配所有以sed开头的行。
$ 匹配行结束，如：/sed$/匹配所有以sed结尾的行。 . 匹配一个非换行符的任意字符，如：/s.d/匹配s后接一个任意字符，最后是d。
* 匹配0个或多个字符，如：/*sed/匹配所有模板是一个或多个空格后紧跟sed的行。 
[] 匹配一个指定范围内的字符，如/[ss]ed/匹配sed和Sed。 
[^] 匹配一个不在指定范围内的字符，如：/[^A-RT-Z]ed/匹配不包含A-R和T-Z的一个字母开头，紧跟ed的行。 
\(..\) 匹配子串，保存匹配的字符，如s/\(love\)able/\1rs，loveable被替换成lovers。 
& 保存搜索字符用来替换其他字符，如s/love/**&**/，love这成**love**。 
\< 匹配单词的开始，如:/\ 匹配单词的结束，如/love\>/匹配包含以love结尾的单词的行。 
x\{m\} 重复字符x，m次，如：/0\{5\}/匹配包含5个0的行。 
x\{m,\} 重复字符x，至少m次，如：/0\{5,\}/匹配至少有5个0的行。 
x\{m,n\} 重复字符x，至少m次，不多于n次，如：/0\{5,10\}/匹配5~10个0的行。
```

# 二、例子

```
#数据的搜寻并替换
sed 's/要被取代的字串/新的字串/g'
/sbin/ifconfig eth0 | grep 'inet addr' | sed 's/^.*addr://g'
# 利用 sed 将 regular_express.txt 内每一行结尾若为 . 则换成 !
sed -i 's/\.$/\!/g' regular_express.txt
#利用 sed 直接在 regular_express.txt 最后一行加入『# This is a test』
sed -i '$a # This is a test' regular_express.txt

#将 /etc/passwd 的内容列出并且列印行号，同时，请将第 2~5 行删除！
nl /etc/passwd | sed '2,5d'
nl /etc/passwd | sed '2d' 
nl /etc/passwd | sed '3,$d' 
#在第二行后(亦即是加在第三行)加上『drink tea?』字样！
nl /etc/passwd | sed '2a drink tea'
#那如果是要在第二行前
nl /etc/passwd | sed '2i drink tea' 
#如果是要增加两行以上，在第二行后面加入两行字，例如『Drink tea or .....』与『drink beer?』
nl /etc/passwd | sed '2a Drink tea or ......\
> drink beer ?'
#搜索 /etc/passwd有root关键字的行
nl /etc/passwd | sed '/root/p'

#正则表达式 \w\+ 匹配每一个单词，使用 [&] 替换它，& 对应于之前所匹配到的单词：
echo this is a test line | sed 's/\w\+/[&]/g'
[this] [is] [a] [test] [line]
# 所有以192.168.0.1开头的行都会被替换成它自已加localhost：
sed 's/^192.168.0.1/&localhost/' file
#匹配给定样式的其中一部分：

echo this is digit 7 in a number | sed 's/digit \([0-9]\)/\1/' 
this is 7 in a number
#命令中 digit 7，被替换成了 7。样式匹配到的子串是 7，\(..\) 用于匹配子串，对于匹配到的第一个子串就标记为 \1，依此类推匹配到的第二个结果就是 \2，例如：
echo aaa BBB | sed 's/\([a-z]\+\) \([A-Z]\+\)/\2 \1/' 
BBB aaa
#love被标记为1，所有loveable会被替换成lovers，并打印出来：

sed -n 's/\(love\)able/\1rs/p' file

#打印奇数行或偶数行
方法1：
 sed -n 'p;n' test.txt  #奇数行 
 sed -n 'n;p' test.txt  #偶数行
方法2： 
sed -n '1~2p' test.txt #奇数行 
sed -n '2~2p' test.txt #偶数行

#一条sed命令，删除/etc/passwd第三行到末尾的数据，并把bash替换为blueshell
#e表示多点编辑，第一个编辑命令删除/etc/passwd第三行到末尾的数据，第二条命令搜索bash替换为blueshell。

nl /etc/passwd | sed -e '3,$d' -e 's/bash/blueshell/'
1  root:x:0:0:root:/root:/bin/blueshell
2  daemon:x:1:1:daemon:/usr/sbin:/bin/sh
```



