## 编码

默认情况下，Python 3 源码文件以**UTF-8**编码，所有字符串都是 unicode 字符串。 当然你也可以为源码文件指定不同的编码：

```
# -*- coding: cp-1252 -*-
```

```
>>> import sys
>>> sys.getdefaultencoding()
'utf-8'
```

使用Python解释器进行如下编码解码操作，在bytes和str之间转换：

```
a = "中国"
b = a.encode()
c = b.decode("utf-8")
print (b)
print (c)

#结果
utf-8
b'\xe4\xb8\xad\xe5\x9b\xbd'
中国
```



