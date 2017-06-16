# python os.path详解

```
import os
import sys
#__file__ 是用来获得模块所在的路径的，这可能得到的是一个相对路径
jms_dir = os.path.dirname(os.path.abspath(os.path.dirname(__file__)))

#对于模块和自己写的程序不在同一个目录下，可以把模块的路径通过sys.path.append(路径)添加到程序中。
sys.path.append(jms_dir)

#获取主执行文件路径的最佳方法是用sys.argv[0]，它可能是一个相对路径，所以再取一下abspath是保险的做法，像这样：

dirname, filename = os.path.split(os.path.abspath(sys.argv[0]))
print (dirname)
print (filename)
```

# 

# os.path详解：

| 方法 | 详解 |
| :--- | :--- |
| os.path.abspath\(path\) | \#返回绝对路径 |
| os.path.basename\(path\) | \#返回文件名 |
| os.path.commonprefix\(list\) | \#返回list\(多个路径\)中，所有path共有的最长的路径。 |
| os.path.dirname\(path\) | \#返回文件路径 |
| os.path.exists\(path\) | \#路径存在则返回True,路径损坏返回False |
| os.path.lexists | \#路径存在则返回True,路径损坏也返回True |
| os.path.expanduser\(path\) | \#把path中包含的"~"和"~user"转换成用户目录 |
| os.path.expandvars\(path\) | \#根据环境变量的值替换path中包含的”$name”和”${name}” |
| os.path.getatime\(path\) | \#返回最后一次进入此path的时间。 |
| os.path.getmtime\(path\) | \#返回在此path下最后一次修改的时间。 |
| os.path.getctime\(path\) | \#返回path的大小 |
| os.path.getsize\(path\) | \#返回文件大小，如果文件不存在就返回错误 |
| os.path.isabs\(path\) | \#判断是否为绝对路径 |
| os.path.isfile\(path\) | \#判断路径是否为文件 |
| os.path.isdir\(path\) | 判断路径是否为目录 |
| os.path.islink\(path\) | \#判断路径是否为链接 |
| os.path.ismount\(path\) | \#判断路径是否为挂载点（） |
| os.path.join\(path1\[, path2\[, ...\]\]\) | \#把目录和文件名合成一个路径 |
| os.path.normcase\(path\) | \#转换path的大小写和斜杠 |
| os.path.normpath\(path\) | \#规范path字符串形式 |
| os.path.realpath\(path\) | \#返回path的真实路径 |
| os.path.relpath\(path\[, start\]\) | \#从start开始计算相对路径 |
| os.path.samefile\(path1, path2\) | \#判断目录或文件是否相同 |
| os.path.sameopenfile\(fp1, fp2\) | \#判断fp1和fp2是否指向同一文件 |
| os.path.samestat\(stat1, stat2\) | \#判断stat tuple stat1和stat2是否指向同一个文件 |
| os.path.split\(path\) | 把路径分割成dirname和basename，返回一个元组 |
| os.path.splitdrive\(path\) | \#一般用在windows下，返回驱动器名和路径组成的元组 |
| os.path.splitext\(path\) | 分割路径，返回路径名和文件扩展名的元组 |
| os.path.splitunc\(path\) | \#把路径分割为加载点与文件 |
| os.path.walk\(path, visit, arg\) | \#遍历path，进入每个目录都调用visit函数，visit函数必须有3个参数\(arg, dirname, names\)，dirname表示当前目录的目录名，names代表当前目录下的所有文件名，args则为walk的第三个参数 |
| os.path.supports\_unicode\_filenames | \#设置是否支持unicode路径名 |

# 其他

Python的标准库中的os模块主要涉及普遍的操作系统功能。可以在Linux和Windows下运行，与平台无关。

os.sep 可以取代操作系统特定的路径分割符。

os.name字符串指示你正在使用的平台。比如对于Windows，它是’nt’，而对于Linux/Unix用户，它是’posix’。

os.getcwd\(\)函数得到当前工作目录，即当前Python脚本工作的目录路径。

os.getenv\(\)和os.putenv\(\)函数分别用来读取和设置环境变量。

os.listdir\(\)返回指定目录下的所有文件和目录名。

os.remove\(\)函数用来删除一个文件。

os.system\(\)函数用来运行shell命令。

os.linesep字符串给出当前平台使用的行终止符。例如，Windows使用’\r\n’，Linux使用’\n’而Mac使用’\r’。

os.listdir\(dirname\)：列出dirname下的目录和文件

os.getcwd\(\)：获得当前工作目录

os.curdir:返回但前目录（’.’\)

os.chdir\(dirname\):改变工作目录到dirname

sys.argv: 实现从程序外部向程序传递参数。

sys.exit\(\[arg\]\): 程序中间的退出，arg=0为正常退出。

sys.getdefaultencoding\(\): 获取系统当前编码，一般默认为ascii。

sys.setdefaultencoding\(\): 设置系统默认编码，执行dir（sys）时不会看到这个方法，在解释器中执行不通过，可以先执行reload\(sys\)，在执行 setdefaultencoding\(‘utf8’\)，此时将系统默认编码设置为utf8。（见设置系统默认编码 ）

sys.getfilesystemencoding\(\): 获取文件系统使用编码方式，Windows下返回’mbcs’，mac下返回’utf-8’.

sys.path: 获取指定模块搜索路径的字符串集合，可以将写好的模块放在得到的某个路径下，就可以在程序中import时正确找到。

sys.platform: 获取当前系统平台。

sys.stdin,sys.stdout,sys.stderr stdin , stdout , 以及stderr 变量包含与标准I/O 流对应的流对象. 如果需要更好地控制输出,而print 不能满足你的要求, 它们就是你所需要的. 你也可以替换它们, 这时候你就可以重定向输出和输入到其它设备\( device \), 或者以非标准的方式处理它们

platform.system\(\) 获取操作系统类型，windows、linux等

platform.platform\(\) 获取操作系统，Darwin-9.8.0-i386-32bit

platform.version\(\) 获取系统版本信息 6.2.0

platform.mac\_ver\(\)

platform.win32\_ver\(\) \(‘post2008Server’, ‘6.2.9200’, ”, u’Multiprocessor Free’\)

