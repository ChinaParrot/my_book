## Python的字符串

在最新的Python 3版本中，字符串是以Unicode编码的，也就是说，Python的字符串支持多语言，例如：

```
>>> print('包含中文的str')
包含中文的str
```

对于单个字符的编码，Python提供了`ord()`函数获取字符的整数表示，`chr()`函数把编码转换为对应的字符：

```
>>> ord('A')
65
>>> ord('中')
20013
>>> chr(66)
'B'
>>> chr(25991)
'文'
```

## python 字符串格式化

python 支持格式化字符串的输出 。尽管这样可能会用到非常复杂的表达式，但最基本的用法是将一个值插入到一个有字符串格式符 %s 的字符串中。

如下实例：

```
#!/usr/bin/python

print "My name is %s and weight is %d kg!" % ('Zara', 21)
#结果
My name is Zara and weight is 21 kg!
```

python字符串格式化符号:

```
%c  格式化字符及其ASCII码
%s  格式化字符串
%d  格式化整数
%u  格式化无符号整型
%o  格式化无符号八进制数
%x  格式化无符号十六进制数
%X  格式化无符号十六进制数（大写）
%f  格式化浮点数字，可指定小数点后的精度
%e  用科学计数法格式化浮点数
%E  作用同%e，用科学计数法格式化浮点数
%g  %f和%e的简写
%G  %f 和 %E 的简写
%p  用十六进制数格式化变量的地址
```

## 常用字符串处理函数

| 函数 | 描述 |
| :--- | :--- |
| len\(s\) | 获取字符串长度 |
| s.upper\(\) | 将字符串全部转换为大写 |
| s.lower\(\) | 将字符串全部转换为小写 |
| s.swapcase\(\) | 将字符串中大写转小写，小写转大写 |
| s.ljust\(30\) | 获取固定长度，右对齐，右边不够用空格补齐 |
| s.rjust\(30\) | 获取固定长度，左对齐，左边不够用空格补齐 |
| s.center\(30\) | 获取固定长度，中对齐，中间不够用空格补齐 |
| s.zfill\(30\) | 获取固定长度，右对齐，右边不够用0补齐 |
| s.find\("要搜索的字符串",start\(可选，起始位置\),end\(可选，结束位置\)\) | 搜索指定字符串，没有返回-1，有的话返回下表开始的位置 |
| s.rfind\("python"\) | 从右边开始搜索 |
| s.count\("p"\) | 统计该字符串出现的次数 |
| s.index\("python"\) | s.index\(\)g跟find\(\)方法一样，只是查不到会抛异常 |
| s.replace\("love","like"\) | 替换s中的love为like |
| s.replace\("python","scala",2\) | 替换s中的python为scala,最后一个参数为替换的次数 |
| s3 = "  i love python    "                                                                  print\(s3.strip\(\)\)                                                                             print\(s3.lstrip\(\)\)                                                                           print\(s3.rstrip\(\)\) | 去两边空格                                                                                    去左边空格                                                                                     去右边空格 |
| s4 = "i love python"                                                                        print\(s4.strip\("i"\)\)                                                                          print\(s4.lstrip\("i"\)\)                                                                         print\(s4.rstrip\("python"\)\) | \#去两边字符串                                                                               去左边字符串                                                                                去右边字符串 |
| print\(s.split\(" "\)\) | 按指定字符分割字符串为数组 |
| print\(s.startswith\("study"\)\) | 是否以study开头 |
| print\(s.endswith\("python"\)\) | 是否以python结尾 |
| print\(s.isalnum\(\)\) | 是否全为字母或数字\(要么全是字母，要么全是数字\) |
| print\(s.isalpha\(\)\) | 是否全为字母 |
| print\(s.isdigit\(\)\) | 是否全为数字 |
| print\(s.islower\(\)\) | 是否全是小写 |
| print\(s.isupper\(\)\) | 是否全是大写 |
| print\(s.istitle\(\)\) | s的首字母是否是大写 |

```
#编解码
#解码函数
print(type(s))
s = s.decode("utf-8")
print(type(s))
#编码函数
s = s.encode("utf-8")
print(type(s))
#cmp函数用于比较两个对象s<s2返回-1，s>s2返回1 s=s2返回0
print(cmp(s1,s2))
```



