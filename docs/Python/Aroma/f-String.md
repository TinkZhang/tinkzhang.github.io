---
layout: default
title: f-string
parent: Python Aroma
grand_parent: Python
---

# f-string

## 为什么需要f-string？

如果我想要在字符串中插入变量，我需要使用`+`运算符来连接字符串和变量，这会使代码变得冗长且难以阅读。

```python
name = "Tink"
age = 18
print("My name is " + name + " and I am " + str(age) + " years old.")
```

f-string是Python 3.6引入的一种格式化字符串的方式，它允许我们在字符串中直接嵌入变量，并且可以在字符串中直接进行运算。

```python
name = "Tink"
age = 18
print(f"My name is {name} and I am {age} years old.")
```

输出：
```
My name is Tink and I am 18 years old.
```

f-string的语法是在字符串前面加上字母f（format的首字母），然后在字符串中用花括号{}括起来要嵌入的变量。Python会自动将花括号中的变量替换为对应的值。

f-string的优点是简洁、易读，并且可以在字符串中直接进行运算。但是f-string也有一些缺点，比如性能较差，并且不支持多行字符串。

## f-string的几个例子

### = 输出表达式
= 能够显示等号左边表达式的字面内容和对应的值。

```python
name = "Tink"
age = 18
print(f"{name=}")
print(f"{age=}")
```
输出：
```
name='Tink'
age=18
```

```python
name = "Tink"
age = 18
print(f"{isinstance(age, int)=}")
```
输出：

```
isinstance(age, int)=True
```

### :格式化数字

保留小数位数
```python
num = 3.1415926
percent = 0.231234
print(f"{num:.2f}")
print(f"{percent:.2%}")
```

输出：
```
3.14
23.12%
```

千位分隔符，支持_ 和 , 两种分隔符
```python
big = 12345678901234567890
print(f"{big:,}")
print(f"{big:_}")
```

输出：
```
1,234,567,890,123,456,789
12_345_678_901_234_567_890
```

两者可以一起使用
```python
big: float = 123456.789
print(f"{big:_.2f}")
```

输出：
```
123_456.79
```

### 格式化日期

```python
from datetime import datetime

now:datetime = datetime.now()
print(f"{now:%x}")
print(f"{now:%c}")
print(f"{now:%Y-%m-%d %H:%M:%S}")
```

输出：

```
11/28/24
Thu Nov 28 01:03:07 2024
2024-11-28 01:03:07
```

### fr字符串

fr字符串可以用来创建包含原始字符串的f-string。在fr字符串中，所有的反斜杠都会被保留，不会被转义。

```python
path = r"C:\Users\Tink\Documents\test.txt"
print(f"File path: {path}")
```

输出：

```
File path: C:\Users\Tink\Documents\test.txt
```

### 填充和对齐
f-string支持填充和对齐，使用`<`、`>`和`^`来指定对齐方式，使用`:`来指定填充字符和宽度。
宽度可以是变量，也可以是固定的数字。填充字符可以是任何字符，默认是空格。

```python
name = "Tink"
print(f"{name:🐱<20}")
print(f"{name:🐶>20}")
print(f"{name:*^20}")
```

输出：
```
Tink🐱🐱🐱🐱🐱🐱🐱🐱🐱🐱🐱🐱🐱🐱🐱🐱
🐶🐶🐶🐶🐶🐶🐶🐶🐶🐶🐶🐶🐶🐶🐶🐶Tink
********Tink********
```

## f-string的原理

f-string是通过调用对象的`__format__`方法来实现的。`__format__`方法接受一个格式化字符串作为参数，返回一个格式化后的字符串。
例如，对于`f"{name:🐱<20}"`，Python会调用`name.__format__(":🐱<20")`，返回一个格式化后的字符串。
知道了原理，我们可以通过重写对象的`__format__`方法来自定义f-string的格式化行为。

```python
class MyString(str):
    def __format__(self, format_spec:str):
        match format_spec:
            case "大写":
                return self.upper()
            case _:
                return super().__format__(format_spec)

name = MyString("tink")
print(f"{name:大写}")
```

输出：
```
TINK
```

参考[Every F-String Trick In Python Explained](https://www.youtube.com/watch?v=9saytqA0J9A)