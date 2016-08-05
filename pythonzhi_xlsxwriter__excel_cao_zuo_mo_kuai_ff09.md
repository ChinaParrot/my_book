# Python之XlsxWriter（Excel操作模块）

1. Workbook类

Workbook类定义：Workbook(filename[, options])，该类实现创建一个XlsxWriter的Workbook对象。Workbook类代表整个电子表格文件，并且存储在磁盘上。参数filename（String类型）为创建的Excel文件存储路径；参数options（Dict类型）为可选的Workbook参数，一般作为初始化工作表内容格式，例如值为{'strings_to_numbers': True}表示使用worksheet.write()方法时激活字符串转换数字。
add_worksheet([sheetname])方法，作用是添加一个新的工作表，参数sheetname（String类型）为可选的工作表名称，默认为Sheet1。

