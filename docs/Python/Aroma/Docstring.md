---
layout: default
title: Docstrings
parent: Python Aroma
grand_parent: Python
---

# Docstrings

```
Docstring: A string literal which appears as the first expression in a class, function or module. While ignored when the suite is executed, it is recognized by the compiler and put into the __doc__ attribute of the enclosing class, function or module. Since it is available via introspection, it is the canonical place for documentation of the object.
```

Docstring是Python中对函数、类或者模块进行说明的文字。和注释不同，Docstring的内容会被编译器识别，并生成__doc__属性。更重要的是，IDE可以识别Docstring，在调用函数、类或者模块的时候，Quick Help窗口能显示Docstring的内容。另外可以通过Docstring，生成完整的API文档。

Docstring的基本用法很简单，对于module，在文件的最开始部分定义；对于class和function，在类或者函数体最开始的地方定义。用三个单引号或者双引号作为开始和结束。如

```python
def add(a: int, b: int) -> int:
    """
    A simple function to add two integers
    """

    return a + b
```

这样，我们在其它地方使用的时候，就能看到这个函数的解释。
![quick-helper](/assets/images/docstring/quick-helper.png)

## Docstring的风格

一般来说，Docstring除了描述，还有需要加上其它的说明，比如函数中每个入参的意义。对于Docstring完整的写法，有几种不同的风格。在PyCharm中，我们还可以指定Docstring的风格。

![docstring-in-pycharm](/assets/images//docstring/docstring-in-pycharm.png)

介绍一下Google的Docstring格式。完整内容见[Google Python Style Guide](https://google.github.io/styleguide/pyguide.html#381-docstrings)

### Module的Docstring

用双引号而非单引号；最直接的解释直接跟在双引号后面，而不是重起一行；可以有更详细的介绍和使用例子。

```python
"""A one-line summary of the module or program, terminated by a period.

Leave one blank line.  The rest of this docstring should contain an
overall description of the module or program.  Optionally, it may also
contain a brief description of exported classes and functions and/or usage
examples.

Typical usage example:

  foo = ClassFoo()
  bar = foo.function_bar()
"""
```

### Function的Docstring

如果函数是public的、或者不是非常简单的、或者逻辑不是很简单的，都必须要有Docstring。
包含Args、Returns和Raises三个部分。

```python
def fetch_smalltable_rows(
    table_handle: smalltable.Table,
    keys: Sequence[bytes | str],
    require_all_keys: bool = False,
) -> Mapping[bytes, tuple[str, ...]]:
    """Fetches rows from a Smalltable.

    Retrieves rows pertaining to the given keys from the Table instance
    represented by table_handle.  String keys will be UTF-8 encoded.

    Args:
        table_handle: An open smalltable.Table instance.
        keys: A sequence of strings representing the key of each table
          row to fetch.  String keys will be UTF-8 encoded.
        require_all_keys: If True only rows with values set for all keys will be
          returned.

    Returns:
        A dict mapping keys to the corresponding table row data
        fetched. Each row is represented as a tuple of strings. For
        example:

        {b'Serak': ('Rigel VII', 'Preparer'),
         b'Zim': ('Irk', 'Invader'),
         b'Lrrr': ('Omicron Persei 8', 'Emperor')}

        Returned keys are always bytes.  If a key from the keys argument is
        missing from the dictionary, then that row was not found in the
        table (and require_all_keys must have been False).

    Raises:
        IOError: An error occurred accessing the smalltable.
    """
```

一般子类override父类的方法，不需要加docstring了。

### Class的Docstring

Class除了方法需要加Docstring，它的attributes也需要加Docstring

```python
class SampleClass:
    """Summary of class here.

    Longer class information...
    Longer class information...

    Attributes:
        likes_spam: A boolean indicating if we like SPAM or not.
        eggs: An integer count of the eggs we have laid.
    """

    def __init__(self, likes_spam: bool = False):
        """Initializes the instance based on spam preference.

        Args:
          likes_spam: Defines if instance exhibits this preference.
        """
        self.likes_spam = likes_spam
        self.eggs = 0

    @property
    def butter_sticks(self) -> int:
        """The number of butter sticks we have."""
```

## 利用Sphinx生成API文档

对于大型的项目，有时候我们需要生产完整的API文档，让别人可以方便地使用我们API。Sphinx可以根据Docstring，生成完整的HTML文档。

具体实现，参考[Sphinx QuickStart](https://www.sphinx-doc.org/en/master/usage/quickstart.html) 和 [Introduction to Sphinx Python Document Generation](https://www.youtube.com/watch?v=nZttMg_n_s0&ab_channel=RealPython)