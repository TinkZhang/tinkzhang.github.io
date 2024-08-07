---
layout: default
title: Optional[int] vs int | None
parent: Python Aroma
grand_parent: Python
---

# Optional[int] vs int | None

声明一个变量时，Python不要求声明变量类型，并且实际上Python中变量的类型是可变的，所以Python是典型的弱类型语言或者叫动态类型语言。

```Python3
num1 = 1
num1 = "a"
```

弱类型的特性可能会导致一些不易察觉的bug，所以在PyCharm这类IDE中，我们可以在声明变量时加上类型，IDE可以帮助我们检查类型。这个时候如果我们改变了类型，IDE会给我们错误提示。但是如果用命令行的方式去执行py文件，还是可以正常执行的。

```Python3
num2: int = 1
num2 = "a"
```

对于可空变量，有两种类型声明的方式

```Python3
num: Optional[int]
num: int | None
```
现在[第二种方式是更为推荐的写法](https://stackoverflow.com/questions/69440494/python-3-10-optionaltype-or-type-none)