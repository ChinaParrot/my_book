# python

查看python排行：  
[http://www.tiobe.com/index.php/tiobe\_index](http://www.tiobe.com/index.php/tiobe_index)

本书全部来自互联网，并经过实践。Python官网：[https://www.python.org/](https://www.python.org/)

本书编写：gitbook  
[https://www.gitbook.com/editor/windows](https://www.gitbook.com/editor/windows)

**服务器环境**

## 1、安装gitbook

```
#ubuntu
apt-get update
apt-get install -y build-essential
curl -sL https://deb.nodesource.com/setup | sudo bash -
apt-get install nodejs
```

```
#centos
#添加epel源
curl --silent --location https://rpm.nodesource.com/setup_5.x | bash -
yum install -y nodejs
```

```
#使用淘宝cnpm
npm install -g cnpm --registry=https://registry.npm.taobao.org
npm config set registry https://registry.npm.taobao.org 
#安装gitbook
cnpm install -g gitbook-cli
#启动服务
gitbook serve
```

## 2、gitbook使用

* 使用 gitbook init 初始化书籍目录
* 使用 gitbook serve 编译书籍

```
mkdir book
gitbook init
#启动服务
gitbook serve
```

## 3、python环境





