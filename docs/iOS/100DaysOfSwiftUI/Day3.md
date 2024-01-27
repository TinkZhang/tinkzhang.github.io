---
layout: default
title: Day 3: 数组/字典/Set/枚举
parent: 100天学会SwiftUI
grand_parent: iOS
---

# 第三天： 数组/字典/Set/枚举

<https://www.hackingwithswift.com/100/swiftui/3>

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

## 字典

```swift
let employee2 = [
    "name": "Taylor Swift",
    "job": "Singer", 
    "location": "Nashville"
]
let olympics = [
    2012: "London",
    2016: "Rio de Janeiro",
    2021: "Tokyo"
]
// 初始化一个空字典
var olympics = [Int, String]()
olympics[2008] = "Beijing"

// 读取字典
print(olympics[2008])
print(olympics[2009, default: "No City"])

// 修改字典
olympics[2008] = "New Beijing"
```
[Dictionary Documentation](https://developer.apple.com/documentation/swift/dictionary)

## Set

```swift
let people = Set(["Denzel Washington", "Tom Cruise", "Nicolas Cage", "Samuel L Jackson"])

var people = Set<String>()
people.insert("Denzel Washington")
people.insert("Tom Cruise")
people.insert("Nicolas Cage")
people.insert("Samuel L Jackson")
```

Set和Array的区别：
1. Set元素是不重复的；
2. Set元素是无序的，所以不能按照index获取元素，虽然Set有`removeFirst()`这样的函数，但是每次remove是随机的；
3. Set的`contains()`函数是`O(1)`，而Array是`O(n)`，本质上因为Set是用Hash值索引，Array是内存中连续位置；
4. Set添加元素是`insert()`，而Array是`append()`。

[Set Documentation](https://developer.apple.com/documentation/swift/set)

## 枚举

```swift
enum Weekday {
    case monday
    case tuesday
    case wednesday
    case thursday
    case friday
}

enum Weekday {
    case monday, tuesday, wednesday, thursday, friday
}

var day = Weekday.monday
// day的类型已经确定，可以省去枚举名
day = .friday
```

[Enum Documentation](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/enumerations/)