# Python之difflib模块对比文件内容差异

通过difflib模块实现文件内容差异对比。difflib作为Python的标准库模块，无需安装。  
实例：

```
#!/usr/bin/env python
#-*- coding:utf-8 -*-
import difflib
import sys

try:
    textfile1 = sys.argv[1]
    textfile2 = sys.argv[2]
except Exception,e:
    print 'Error:'+str(e)
    print "Usage: %s filename1 filename2" % sys.argv[0]
    sys.exit()
def readfile(filename): #文件读取分隔函数
    try:
        fileHandle = open (filename,'rb')
        text = fileHandle.read().splitlines() #读取后进行分隔
        fileHandle.close()
        return text
    except IOError as error:
        print ('Read file Error:' + str(error))
        sys.exit()
if textfile1 == "" or textfile2 == "":
    print "Usage: %s filename1 filename2" % sys.argv[0]
    sys.exit()
text1_lines = readfile(textfile1) #调用readfile函数，获取分隔后的字符串
text2_lines = readfile(textfile2)

d = difflib.HtmlDiff() #创建HtmlDiff()对象
print d.make_file(text1_lines,text2_lines)
```



