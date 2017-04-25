Linux系统中grep命令是一种强大的文本搜索工具，它能使用正则表达式搜索文本，并把匹 配的行打印出来。grep全称是Global Regular Expression Print，表示全局正则表达式版本，它的使用权限是所有用户。

主要参数：

grep  \[options\]

```
-a 不要忽略二进制数据。
-A<显示列数> 除了显示符合范本样式的那一行之外，并显示该行之后的内容。
-B<显示行数>   --before-context=<显示行数>   #除了显示符合样式的那一行之外，并显示该行之前的内容。   
-f<规则文件>  --file=<规则文件>   #指定规则文件，其内容含有一个或多个规则样式，让grep查找符合规则条件的文件内容，格式为每行一个规则样式。 
-d<进行动作> 当指定要查找的是目录而非文件时，必须使用这项参数，否则grep命令将回报信息并停止动作。
- c：只输出匹配行的计数。
- i：搜索时忽略大小写。 
- I：不区分大 小写(只适用于单字符)。
- h：查询多文件时不显示文件名。
- l：查询多文件时只输出包含匹配字符的文件名。
- n：显示匹配行及 行号。
- s：不显示不存在或无匹配文本的错误信息。
- v：显示不包含匹配文本的所有行。
- w：匹配整词。
- x：匹配整行。
- r：递归搜素，不仅搜素当前目录，而且搜素子目录。
- q：禁止输出任何结果，以退出状态表示搜素是否成功。 
- b：打印匹配行距文件头部的偏移量，以字节为单位。
- o：与-b选项结合使用，打印匹配的词距文件头部的偏移量，以字节为单位。
- E：支持扩展的正则表达式。
- F：不支持正则表达式，按照字符串的字面意思进行匹配。
-G   --basic-regexp   #将样式视为普通的表示法来使用。   
-L   --files-without-match   #列出文件内容不符合指定的样式的文件名称。
```

例子：

```
#搜索和寻找文件
sudo dpkg -l | grep -i python 
#搜索和过滤文件
sudo grep -v "#" /etc/apache2/sites-available/default-ssl 
#找出所有的mp3文件
sudo find . -name ".mp3" | grep -i JayZ | grep -vi "remix"" 
#在搜索字符串前面或者后面显示行号
sudo ifconfig | grep -A 4 eth0 
sudo ifconfig | grep -B 2 UP 
#进行精确匹配搜索
ifconfig | grep -w “RUNNING” 
ifconfig | grep -w “RUN”
#将/etc/passwd，有出现 root 的行取出来,同时显示这些行在/etc/passwd的行号
grep -n root /etc/passwd

```



