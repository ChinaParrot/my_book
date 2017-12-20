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

任何你可用 “for… in…” 处理的都是可迭代对象：列表，字符串，文件….这些迭代对象非常便捷，因为你可以尽可能多地获取你想要的东西



