# Python yield 使用

## 迭代 {#_1}

你可以创建一个列表，然后逐一遍历，这就是迭代

```
>>> mylist = [1, 2, 3]
>>> for i in mylist:
...    print(i)
1
2
3

```



例如：以上xrange怎么实现？

```
def foo():
    yield 1
    yield 2
    yield 3
    yield 4
    re = foo()
    #print re
    for item in re:
        print item
```

```
def Readline():
    seek = 0
    while True:
        with open("test.txt",'r') as f:
        f.seek(seek)
    data = f.readline()
    if data:
        seek = f.tell()
        yield data
    else
        return
    for item in Readline():
        print (item)
```



