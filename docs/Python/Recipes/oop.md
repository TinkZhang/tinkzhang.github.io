---
layout: default
title: OOP
parent: Python Recipes
grand_parent: Python
---

# Python的面相对象

## Class

用class关键字声明类；用Animal()生成一个对象。

```python
class Animal:
    pass

cat: Animal = Animal()
```

## Attribute和Property

Python动态语言特性，设计的attribute不一定要在class中定义的，比如下面的代码，可以有了cat这个对象，再给cat添加name属性。

```python
cat.name = "Foo"
print(cat.name)
```

也可以在class中定义attribute，下面的sel.name就定义了name这个属性。

```python
class Animal:
    def __init__(self, name):
        self.name = name
```

可以通过__slots__方法，限定类的属性，这样就不能随意添加新属性了，能节省内存。

```python
class Point:
    __slots__ = ['x', 'y']

    def __init__(self, x, y):
        self.x = x
        self.y = y

p = Point(1, 2)
p.z = 3  # ❌ 抛出 AttributeError
```

Python attribute的没有真正的访问限制，是通过命名规则来实现。一个下划线是protected，但是IDE只是通过命名规则来检测并提醒；两个下划线是private，直接调用编译就会出错了，但是仍可以通过._ClassName__attribute来获取。

```python
class Animal:
    def __init__(self, name, age):
        self._hidden_name = name
        self.__age = age

cat: Animal = Animal("Foo", 16)
cat._hidden_name # ⚠️ IDE Warning, _hidden_name是protected
cat.__age        # ❌ Error, __age是private
cat._Animal__age # 仍能通过这种方式获取private的属性
```

为了给private attribute提供外部读写的途径，Python有Property的概念。通过@property声明

```python
class Animal:
    def __init__(self, hidden_name):
        self.__hidden_name = hidden_name

    @property
    def name(self):
        return self.hidden_name

    @name.setter
    def name(self, input_name):
        self.hidden_name = input_name

cat: Animal = Animal("Foo")
print(cat.name)  # 会调用property的name函数
cat.name = "Bar" # 会调用setter的name函数
```

## Method

Python中实例方法第一个参数为self，即使没有需要传递的参数，也得搞个self。

```python
class Animal:
    def __init__(self, hidden_name):
        self.__hidden_name = hidden_name

    def eat(self):
        pass
```

静态方法通过添加@staticmethod实现，静态方法不需要加self

```python
class MathUtils:
    @staticmethod
    def add(a: int, b: int) -> int:
        return a + b

MathUtils.add(1 + 2)
```

方法的访问权限和属性类似，通过添加下划线来实现private，但仍可通过._ClassName__method()访问。

## Instance成员 vs Class成员

下面代码中，total_users是Class attribute，username是Instance attribute。Class属性的引用可以通过类名，也可以通过实例；但是修改必须通过类名引用。

```python
class User:
    # 类属性：记录创建了多少个用户
    total_users = 0

    def __init__(self, username):
        self.username = username         # 实例属性
        User.total_users += 1            # 修改类属性

    def show_info(self):
        print(f"Username: {self.username}")

# 创建几个用户
u1 = User("Alice")
u2 = User("Bob")
u3 = User("Charlie")

# 查看类属性
print(User.total_users)      # 输出: 3

# 也可以通过实例访问类属性
print(u1.total_users)        # 输出: 3
print(u2.total_users)        # 输出: 3
```

下面代码中，添加了@classmethod的from_json是Class方法，第一个参数习惯用cls，代表类。Class方法一般用于创建、操作类本身的逻辑，比如工厂方法。

```python
class User:
    def __init__(self, username, email, created_at=None):
        self.username = username
        self.email = email
        self.created_at = created_at if created_at else datetime.now()

    @classmethod
    def from_json(cls, data):
        """
        工厂方法：从字典数据（如 JSON）构建 User 实例
        """
        return cls(
            username=data.get('username'),
            email=data.get('email'),
            created_at=datetime.fromisoformat(data.get('created_at'))
        )
```

## Magic Method

Python中定义了一些两个下划线开始和结尾的类方法，他们有着自己特殊的能力。

### __init__ 和 __new__

__init__: 初始化器，在对象被创建后，对对象进行初始化。

__new__: 创建一个对象，注意和__init__的区别。它是类的方法，第一个参数是cls，控制对象的创建过程，必须返回一个对象实例。最常用的地方是创建单例。

```python
class MyClass:
    def __new__(cls, *args, **kwargs):
        print("__new__ 被调用")
        instance = super().__new__(cls)  # 创建实例
        return instance

    def __init__(self, value):
        print("__init__ 被调用")
        self.value = value
```

### __str__ 和 __repr__

这两个方法的返回值都是str

__str__: 类似于Java中的toString()方法，一般给用户看

__repr__: 是representation，literally representation，一般给程序员看，比如显示所有的属性

### 其它Magic Method

其它的Magic Method包括算术相关的、上下文管理相关、容器相关和属性访问等。完整的列表见 [Python Special Methods](https://docs.python.org/3/reference/datamodel.html#special-method-names)

```python
__add__(self, other)     # ➕的运算
__lt__(self, other)      # < 的运算
__getattr__(self, name)  # 访问不存在属性时调用
__len__(self)            # len(obj)
__enter__(self)          # 在 with 块开始时调用
__bool__(self)           # 返回布尔值（用于 if obj:）
```

## Inheritance

Python的继承语法比较特别。Python可以继承多个父类。方法的重写是自动识别的，没有override关键字，直接定义同名方法即可。

```python
class Pet:
    pass

class Animal:
	pass

class Cat(Animal, Pet):
	pass
```

## Abstract Class

Python的抽象类有点抽象，需要引入额外的包。ABC是抽象类的基类，所有的抽象类都是继承ABC或者其后代类。@abstractmethod标记抽象方法。

```python
from abc import ABC, abstractmethod

class Animal(ABC):
    @abstractmethod
    def speak(self):
        pass
```

## Protocal

Protocol是一个特殊的类，定义一个Protocol需要继承Protocol这个类。一个类“实现”这个Protocol是完全隐式的，没有implement关键字，也不需要继承，只需要默默地实现Protocol中的方法和属性。

```python
from typing import Protocol

class Printable(Protocol):
		pages: int
		
		def print(self):
				pass
				
		def recycle(self):
				pass
				
class Book:
		pages: int
		
		def __init__(self, pages:str):
				self.pages = pages
		
		def print(self):
				print("Printing book:", self.title)
				
		def recycle(self):
				print("Recycling book:", self.title)

book: Pritable = Book('Python')
```

## Data Class

数据类，帮我们实现了init，eq，repr这些方法。

```python
from dataclasses import dataclass

@dataclass
class Fruit:
		name: str
		colaries: int
```
