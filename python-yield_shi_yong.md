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

mylist是可迭代的对象，当你使用列表解析时，你创建一个列表,即一个可迭代对象

```
>>> mylist = [x*x for x in range(3)]
>>> for i in mylist:
...    print(i)
0
1
4
```

任何你可用 “for… in…” 处理的都是可迭代对象：列表，字符串，文件….这些迭代对象非常便捷，因为你可以尽可能多地获取你想要的东西,但，当你有大量数据并把所有值放到内存时，这种处理方式可能不总是你想要的

## 生成器 {#_2}

生成器是迭代器，但你只能遍历它一次\(iterate over them once\)因为生成器并没有将所有值放入内存中，而是实时地生成这些值

```
>>> mygenerator = (x*x for x in range(3))
>>> for i in mygenerator:
...    print(i)
0
1
4
```

这和使用列表解析地唯一区别在于使用\(\)替代了原来的\[\]

注意，你不能执行for i in mygenerator第二次，因为每个生成器只能被使用一次: 计算0，并不保留结果和状态，接着计算1，然后计算4，逐一生成

## yield {#yield}

  


yield是一个关键词，类似return, 不同之处在于，yield返回的是一个生成器

