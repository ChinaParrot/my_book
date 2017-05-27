# Python yield 使用

```
print range(10)
print xrange(10) #只是生成器，只有遍历的时候创建

for item in xrange(10):
    print (item)
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
print item
```



