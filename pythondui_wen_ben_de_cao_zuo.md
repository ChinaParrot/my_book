# python对文件操作

**文件的读取**

```
>>> f=file('contact_list.txt','a')
>>> f.write('\n26\tLizhili\tIt\t2222222222')
>>> f.close
```

```
#!/usr/bin/python3
import sys
contact_list='contact_list.txt'
f=file(contact_list)
c=f.readlines()
while True:
    user_input = input('\033[0;31;1m please input sth to search: \033[0m')
    if len(user_input) == 0:
        continue
    for line in c:
        if user_input in line:
            print (line)
        elif user_input == "a" or user_input == "quit":
            sys.exit()
    else:
        print ("\033[1;32m not in world key word! \033[0m")
```

**文件修改和替换**

```
#/usr/bin/python
import fileinput
for line in fileinput.input('user.txt',inplace=1):
    line =line.replace('1',"001")
    print line
```

Python中对文件、文件夹（文件操作函数）的操作需要涉及到os模块和shutil模块。

获取操作系统名字os.name\(\)

如果是posix，说明系统是Linux、Unix或Mac OS X，如果是nt，就是Windows系统。要获取详细的系统信息，可以调用uname\(\)函数

在操作系统中定义的环境变量，全部保存在os.environ这个dict中，可以直接查看

要获取某个环境变量的值，可以调用os.getenv\(\)函数

```
os.getenv('PATH')
```

**其他函数**

* 得到当前工作目录，即当前Python脚本工作的目录路径：os.getcwd\(\)
* 返回指定目录下的所有文件和目录名：os.listdir\(\)
* 函数用来删除一个文件：os.remove\(\)
* 删除多个目录：os.removedirs\(r"c:\python"\)
* 检验给出的路径是否是一个文件：os.path.isfile\(\)
* 检验给出的路径是否是一个目录：os.path.isdir\(\)
* 判断是否是绝对路径：os.path.isabs\(\)
* 检验给出的路径是否真地存在: os.path.exists\(\)
* 返回一个路径的目录名和文件名：os.path.split\(\)
* 分离扩展名：os.path.splitext\(\)
* 获取路径名：os.path.dirname\(\)
* 运行shell命令：os.system\(\)
* 读取和设置环境变量：os.getenv\(\) 与os.putenv
* 给出当前平台使用的终止符：os.linesep windows使用'\r\n',linux使用'\n' 而mac使用'\r'指示你正在使用的平台：os.name 对于windows,它是'nt',而对于Linux/unix用户而言他是'posix'
* 重命名：os.rename\(old,new\)
* 创建多级目录：os.makedirs\(r"c:\python\test"\)
* 创建单个目录：os.makedir\("test"\)
* 删掉一个目录： os.rmdir\('testdir'\)
* 获取文件属性：os.stat\(file\)
* 修改文件权限=与时间戳：os.chmod\(file\)
* 终止当前进程：os.exit\(\)
* 获取文件大小：os.path.getsize\(filename\)
* 文件操作：
* os.mknod\("test.txt"\) 创建空文件
* fp=open\("test.txt",w\)直接打开一个文件，如果文件不存在则创建文件
* open模式
* w 写方式打开
* a 以追加模式打开（从EOF开始，必要时创建新文件）
* r+ 以读写模式打开
* w+ 以读写模式打开 （参见w）
* a+ 以读写模式打开 \( 参见a\)
* rb 以二进制读模式打开
* wb 以二进制写模式打开
* fp.read\(\[size\]\) \#size位读取的长度，以byte为单位
* fp.readline\(\[size\]\) \#把文件没一行作为一个list的一个成员，并返回这个list。
* 其实他的内部是通过循环调用readline（）来实现的。如果提供size参数，size是读取内容的总长，也就是说可能只读到文件的一部分。
* fp.write\(str\) \#把str写到文件中，write（）并不会在str后加上一个换行符。写入utf8例如：
* fp.write\(str.encode\('utf-8'\)\)
* fp.writelines\(seq\) \#把seq的内容全部写到文件中（多行一次性写入）。这个函数也只是忠实的写入，不会在每行后面加上任何东西。
* fp.close\(\)
* 这一功能没有保证，最好还是养成自己关闭的习惯。如果一个文件在关闭后还对其操作会产生valueerror
* fp.flush\(\) \#把缓冲区的内容写入到磁盘
* fp.fileno\(\)\#返回一个长整形的“文件标签”
* fp.isatty\(\)\#文件是否是一个终端设备文件
* fp.tell\(\)\#返回文件操作标记的当前位置，以文件的开头为原点。
* fp.truncate\(\[size\]\) 截取文件大小

**文件处理的分割  
**

```
f = file('test.txt','r')
f.readline().strip('\n').split()
#split() 列表
#去掉结尾换行符、空格分割。
```

当文件被读取的时候，这时也被写入，可以通过read\(\)读取刚刚写入的内容。

例如：

```
f=open('file.txt',rw)
f.read\(\)
```



