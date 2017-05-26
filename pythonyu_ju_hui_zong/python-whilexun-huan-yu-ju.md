Python 编程中 while 语句用于循环执行程序，即在某条件下，循环执行某段程序，以处理需要重复处理的相同任务。其基本形式为：

while 判断条件：

执行语句……

例子：

```
#!/usr/bin/python3
count = 0
while (count <20):
    print ('The count is:', count)
    count = count + 2
    print ('Good bye!')

```

while 语句时还有另外两个重要的命令 continue，break 来跳过循环，continue 用于跳过该次循环，break 则是用于退出循环，此外"判断条件"还可以是个常值，表示循环必定成立，具体用法如下：

