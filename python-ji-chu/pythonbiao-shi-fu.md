## Python 标识符

在python里，标识符有字母、数字、下划线组成。

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
>>> import keyword
>>> keyword.kwlist
['False', 'None', 'True', 'and', 'as', 'assert', 'break', 'class', 'continue', 'def', 'del', 'elif', 'else', 'except', 'finally', 'for', 'from', 'global', 'if', 'import', 'in', 'is', 'lambda', 'nonlocal', 'not', 'or', 'pass', 'raise', 'return', 'try', 'while', 'with', 'yield']
```



