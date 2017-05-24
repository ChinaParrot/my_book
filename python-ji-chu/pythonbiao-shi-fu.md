## Python 标识符

是用于识别变量、函数、类、模块以及其他对象的名字，标识符可以包含字母、数字及下划线\(\_\)，但是必须以一个非数字字符开始。字母仅仅包括ISO-Latin字符集中的A–Z和a–z。标识符对大小写敏感的，因此 FOO和foo是两个不同的对象。特殊符号，如$、%、@等，不能用在标识符中。另外，如if，else，for 等单词是保留字，也不能将其用作标识符。



python里，标识符有字母、数字、下划线组成。

在python中，所有标识符可以包括英文、数字以及下划线（\_），但不能以数字开头。

python中的标识符是区分大小写的。

## Python保留字符

具有特定意义的字符串，通常也称为保留字。用户定义的标识符不应与关键字相同

| 保留字 | 保留字 | 保留字 |
| --- | --- | --- |
| assert | finally | or |
| and | exec | not |
| break | for | pass |
| class | from | print |
| continue | global | raise |
| del | if | return |
| elif | import | try |
| in | while | else |
| is | with | except |
| lambda | yield | def |

```
import keyword
print (keyword.kwlist)
print (keyword.iskeyword("from"))

#结果:
['False', 'None', 'True', 'and', 'as', 'assert', 'break', 'class', 'continue', 'def', 'del', 'elif', 'else', 'except', 'finally', 'for', 'from', 'global', 'if', 'import', 'in', 'is', 'lambda', 'nonlocal', 'not', 'or', 'pass', 'raise', 'return', 'try', 'while', 'with', 'yield']
True
```



