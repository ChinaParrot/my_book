# Python之XlsxWriter（Excel操作模块）


以下演示基本excel操作

```
#!/usr/bin/env python
#-*- coding:utf-8 -*-

import xlsxwriter

workbook = xlsxwriter.Workbook('demo1.xlsx') #创建一个Excel文件
worksheet = workbook.add_worksheet()  #创建一个工作表对象
worksheet.set_column("A:A",20) #设定第一列（A）宽度为20像素

bold = workbook.add_format({'bold':True}) #定义一个加粗的格式对象
worksheet.write('A1','Hello') #A1单元格写入'Hello'
worksheet.write('A2', 'World', bold)    #A2单元格写入'World'并引用加粗格式对象bold
worksheet.write('B2', u'中文测试', bold)    #B2单元格写入中文并引用加粗格式对象bold

worksheet.write(2, 0, 32)    #用行列表示法写入数字'32'与'35.5'
worksheet.write(3, 0, 35.5)    #行列表示法的单元格下标以0作为起始值，'3,0'等价于'A3'
worksheet.write(4, 0, '=SUM(A3:A4)')    #求A3:A4的和，并将结果写入'4，0'，即'A5'

worksheet.insert_image('E10', 'img/python-logo.png')    #在B5单元格插入图片
workbook.close()    #关闭Excel文件
```

1. Workbook类

Workbook类定义：Workbook(filename[, options])，该类实现创建一个XlsxWriter的Workbook对象。Workbook类代表整个电子表格文件，并且存储在磁盘上。参数filename（String类型）为创建的Excel文件存储路径；参数options（Dict类型）为可选的Workbook参数，一般作为初始化工作表内容格式，例如值为{'strings_to_numbers': True}表示使用worksheet.write()方法时激活字符串转换数字。
add_worksheet([sheetname])方法，作用是添加一个新的工作表，参数sheetname（String类型）为可选的工作表名称，默认为Sheet1。

例如：

``` 
worksheet1 = workbook.add_worksheet()             # Sheet1
worksheet2 = workbook.add_worksheet('Foglio2')    # Foglio2
worksheet3 = workbook.add_worksheet('Data')       # Data
worksheet4 = workbook.add_worksheet()             # Sheet4

```