---
layout: default
title: Day 3
parent: 100天学会SwiftUI
grand_parent: iOS
---

# 数组/字典/集合/枚举
## 数组
### 创建数组
```swift
// 有初始值
var arr = [1,2,3]

// 无初始值两种方式
var arr = Array<Int>()
var arr = [Int]()
```

### 数组的大小
Swift的数组大小是默认是`dynamic`，所以可以`append()`添加新元素。假设初始化的时候给一个元素，它的size是1，但是capacity是4；如果添加到5个，capacity会变成8。每次添加元素遇到满了的情况，capacity都会翻倍，然后把前面的元素复制到新的capacity中。

如果我们知道数组需要增长，可以使用`reserveCapacity(_:)`方法来设置capacity，相当于预分配内存。减少内存分配次数，提高性能。如果后续添加元素超过了预分配的内存，会自动按照翻倍的模式分配新的内存。
```swift
var numbers = [Int]()
numbers.reserveCapacity(400) 
// array size = 0
// capacity = 400
```

### 数组的常用属性和方法
```swift
// 大小
print(albums.count)

// 指定位置删除
characters.remove(at: 2)


// 清除
characters.removeAll()

// 包含判定
bondMovies.contains("Frozen")

// 排序
cities.sorted()

// 反转
presidents.reversed()
```