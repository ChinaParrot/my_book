
# python(2.0)
查看python排行：
http://www.tiobe.com/index.php/tiobe_index


本书全部来自互联网，并经过实践。Python官网：https://www.python.org/

本书编写：gitbook
https://www.gitbook.com/editor/windows


**服务器环境**

# 1、安装gitbook


```

apt-get update
apt-get install -y build-essential
curl -sL https://deb.nodesource.com/setup | sudo bash -
apt-get install nodejs
npm install gitbook -g 

```

# 2、gitbook使用

1、使用 gitbook init 初始化书籍目录<br />
2、使用 gitbook serve 编译书籍<br />

mkdir book
gitbook init
#启动服务
gitbook serve
