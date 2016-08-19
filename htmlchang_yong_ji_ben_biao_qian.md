# HTML常用基本标签

| 标签 | 介绍|
| -- | -- |
| ```<html>``` | HTML页面跟标签 |
|```<title>```|页面标题标签|
|```<head>```|页面头部标签|
|```<body>```|页面体标签|
|```<h>```|标题标签|
|```<p>```|段落标签|
|```<ul>```|无序列表|
|```<ol>```|有序列表|
|```<li>```|列表项|
|```<a>```|超链接标签|
|```<img>```|图片标签|

例子：

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>跑马灯</title>
</head>
<body bgcolor="#f0ffff">
<div align="center">
    <h1><span style="color: black; ">我的相册</span></h1>
    <hr>
    <div style="height: 130px;line-height: 150px;background-color:seashell;padding: 20px">
        <marquee>
            <span>
           <a href="#"><img src="../static/test.jpg" width="200" height="120"></a>
            </span>
        </marquee>

    </div>
</div>


</body>
</html>
```