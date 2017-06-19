# Django基础安装

## 让我们一览 Django 全貌

### urls.py

网址入口，关联到对应的views.py中的一个函数（或者generic类），访问网址就对应一个函数。

### views.py

处理用户发出的请求，从urls.py中对应过来, 通过渲染templates中的网页可以将显示内容，比如登陆后的用户名，用户请求的数据，输出到网页。

### models.py

与数据库操作相关，存入或读取数据时用到这个，当然用不到数据库的时候 你可以不使用。

### forms.py

表单，用户在浏览器上输入数据提交，对数据的验证工作以及输入框的生成等工作，当然你也可以不使用。

### templates 文件夹

views.py 中的函数渲染templates中的Html模板，得到动态内容的网页，当然可以用缓存来提高速度。

admin.py  
后台，可以用很少量的代码就拥有一个强大的后台。

settings.py  
Django 的设置，配置文件，比如 DEBUG 的开关，静态文件的位置等。

## Django 环境搭建

### 1. 通过pip安装：

ubuntu类：

`apt-get install  python-pip           
pip install Django==1.9.6`

Fedora类：

`yum install python-pip`

其他：  
[https://pip.pypa.io/en/latest/installing/](https://pip.pypa.io/en/latest/installing/)  
下载：[get-pip.py](https://bootstrap.pypa.io/get-pip.py)  
然后运行在终端运行 python get-pip.py 就可以安装 pip。

检查安装：

```
>>> import django
>>> print(django.VERSION)
(1, 9, 6, 'final', 0)
```

如果想升级 pip 可以用：

pip install --upgrade pip

### 2. 通过源码安装

```
git clone https://github.com/django/django.git
cd django
python setup.py install
```

# 项目[https://www.djangosites.org/](https://www.djangosites.org/)

### 3、虚拟环境使用

开发会用 virtualenv 来管理多个开发环境，virtualenvwrapper 使得virtualenv变得更好用

pip install virtualenv virtualenvwrapper

Linux/Mac OSX 下：

修改~/.bash\_profile或其它环境变量相关文件\(如 .bashrc 或用 ZSH 之后的 .zshrc\)，添加以下语句

`export WORKON_HOME=$HOME/.virtualenvs`

`export PROJECT_HOME=$HOME/workspace`

`source /usr/local/bin/virtualenvwrapper.sh`

修改后使之立即生效\(也可以重启终端使之生效\)：

source ~/.bash\_profile



使用方法：

mkvirtualenv zqxt：创建运行环境zqxt

workon zqxt: 工作在 zqxt 环境 或 从其它环境切换到 zqxt 环境

deactivate: 退出终端环境

其它的：

rmvirtualenv ENV：删除运行环境ENV

mkproject mic：创建mic项目和运行环境mic

mktmpenv：创建临时运行环境

lsvirtualenv: 列出可用的运行环境

lssitepackages: 列出当前环境安装了的包

创建的环境是独立的，互不干扰，无需sudo权限即可使用 pip 来进行包的管理。



