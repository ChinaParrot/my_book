# 表格标签与布局

##表格标签

``````
<table> //表格标签
<tr> //行标签
<td> //单元格
<th> //th 元素内部的文本通常会呈现为居中的粗体文本，而 td 元素内的文本通常是左对齐的普通文本。
``````

例子：
```
<th>这是个表格实例</th>
<table border="1" width="600" height="50" cellspacing="0" cellpadding="0" bgcolor="#ccffff">
  <tr>
    <td align="center">北京</td>
    <td align="center">上海</td>
  </tr>
  <tr>
    <td>北京</td>
    <td bgcolor="green">上海</td>
  </tr>
</table>
```


##跨行与跨列

```
rowspan //跨行
colspan //跨列
```

例子：
```
<th>这是个表格跨列实例</th>
<table border="1" width="600" height="50" cellspacing="0" cellpadding="0" bgcolor="#ccffff">
  <tr>
    <td align="center" colspan="2">北京</td>
  </tr>
  <tr>
    <td>北京</td>
    <td bgcolor="green">上海</td>
  </tr>
</table>
```

```
<th>这是个表格跨行实例</th>
<table border="1" width="600" height="50" cellspacing="0" cellpadding="0" bgcolor="#ccffff">
  <tr>
    <td align="center" rowspan="2">北京</td>
    <td>上海</td>
  </tr>
  <tr>
    <td bgcolor="green">上海</td>
  </tr>
</table>
```

##表格布局 

```
<!DOCTYPE html>
<html>
<head> 
<meta charset="utf-8"> 
<title>菜鸟教程(runoob.com)</title> 
</head>
<body>

<table width="500" border="0">
<tr>
<td colspan="2" style="background-color:#FFA500;">
<h1>主要的网页标题</h1>
</td>
</tr>

<tr>
<td style="background-color:#FFD700;width:100px;">
<b>菜单</b><br>
HTML<br>
CSS<br>
JavaScript
</td>
<td style="background-color:#eeeeee;height:200px;width:400px;">
内容在这里</td>
</tr>

<tr>
<td colspan="2" style="background-color:#FFA500;text-align:center;">
版权 © runoob.com</td>
</tr>
</table>

</body>
</html>
```