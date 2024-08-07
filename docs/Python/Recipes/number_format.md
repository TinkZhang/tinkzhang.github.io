---
layout: default
title: 数字格式
parent: Python Recipes
grand_parent: Python
---

# 数字格式

给定一个数字，要求输出，保留两位小数，添加千位分隔符

```python
num: float = 1234567.8954
print(f"the number is {num:,.2f}")
# the number is 1,234,567.90
```

Try it on [playground](https://programiz.pro/ide/python)