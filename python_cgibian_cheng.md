# Python CGI编程

**什么是CGI                    
**

CGI 目前由NCSA维护，NCSA定义CGI如下：

CGI\(Common Gateway Interface\),通用网关接口,它是一段程序,运行在服务器上如：HTTP服务器，提供同客户端HTML页面的接口。

**网页浏览                    
**

为了更好的了解CGI是如何工作的，我们可以从在网页上点击一个链接或URL的流程：

1. 使用你的浏览器访问URL并连接到HTTP web 服务器。&lt;br&gt;

2. Web服务器接收到请求信息后会解析URL，并查找访问的文件在服务器上是否存在，如果存在返回文件的内容，否则返回错误信息。

3. 浏览器从服务器上接收信息，并显示接收的文件或者错误信息。CGI程序可以是Python脚本，PERL脚本，SHELL脚本，C或者C++程序等。

**Web服务器支持及配置**

在你进行CGI编程前，确保您的Web服务器支持CGI及已经配置了CGI的处理程序。

Apache 支持CGI 配置：

设置好CGI目录：

```
ScriptAlias /cgi-bin/ /var/www/cgi-bin/
```

所有的HTTP服务器执行CGI程序都保存在一个预先配置的目录。这个目录被称为CGI目录，并按照惯例，它被命名为/var/www/cgi-bin目录。

CGI文件的扩展名为.cgi，python也可以使用.py扩展名。

默认情况下，Linux服务器配置运行的cgi-bin目录中为/var/www。

如果你想指定其他运行CGI脚本的目录，可以修改httpd.conf配置文件，如下所示：

```
<Directory "/var/www/cgi-bin">

AllowOverride None

Options +ExecCGI

Order allow,deny

Allow from all

</Directory>
```

在 AddHandler 中添加 .py 后缀，这样我们就可以访问 .py 结尾的 python 脚本文件：

`AddHandler cgi-script .cgi .pl .py`

**第一个CGI程序**

我们使用Python创建第一个CGI程序，文件名为hello.py，文件位于/var/www/cgi-bin目录中，内容如下，修改文件的权限为755

```
#!/usr/bin/python
# -*- coding: UTF-8 -*-

print ("Content-type:text/html\r\n\r\n")
print ('<html>')
print ('<head>')
print ('<title>Hello Word - First CGI Program</title>')
print ('</head>')
print ('<body>')
print ('<h2>Hello Word! This is my first CGI program</h2>')
print ('</body>')
print ('</html>')
```

以上程序在浏览器访问显示结果如下:

```
Hello Word! This is my first CGI program
```

这个的hello.py脚本是一个简单的Python脚本，脚本第一行的输出内容"Content-type:text/html\r\n\r\n"发送到浏览器并告知浏览器显示的内容类型为"text/html"。

**HTTP头部**

hello.py文件内容中的" Content-type:text/html\r\n\r\n"即为HTTP头部的一部分，它会发送给浏览器告诉浏览器文件的内容类型。

HTTP头部的格式如下：

HTTP 字段名: 字段内容

例如

`Content-type: text/html\r\n\r\n`

以下表格介绍了CGI程序中HTTP头部经常使用的信息：

| 头 | 描述 |
| -- | -- |
|Content-type:| 请求的与实体对应的MIME信息。例如: Content-type:text/html|
|Expires: Date  |响应过期的日期和时间|
|Location: URL| 用来重定向接收方到非请求URL的位置来完成请求或标识新的资源|
|Last-modified: Date|   请求资源的最后修改时间|
|Content-length: N| 请求的内容长度|
|Set-Cookie: String |设置Http Cookie|

**CGI环境变量**

所有的CGI程序都接收以下的环境变量，这些变量在CGI程序中发挥了重要的作用：



