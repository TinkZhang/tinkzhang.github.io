---
layout: default
title: Day 1
parent: 100天学会SwiftUI
grand_parent: iOS
---

# 第一天：Swift的变量，常量，字符串和数字

Link: https://www.hackingwithswift.com/100/swiftui/1

## 变量

创建变量，通过关键字`var`

```swift
// Create a variable
var greeting = "Hello, world"

// Change the variable
greeting = "Hello, Tink"
```

## 常量

创建常量，通过关键字`let`

```swift
// Create a const
let myName = "Tink"

// Change the const will cause error
myName = "Tank"
```

**Swift习惯使用CamelCase命名变量。**

## 字符串

```swift
// 单行字符串
let result = "⭐️ You win! ⭐️"

// 转译符号
let quote = "Then he tapped a sign saying \"Believe\" and walked away."

// 多行字符串用三个“
let movie = """
A day in
the life of an
Apple engineer
"""
// ⚠️ 三引号要自己占一行
```

### 字符串的属性和方法

```swift
// 长度
print(result.count)

// 大小写
print(result.uppercased())
print(result.lowercased())

// 词缀
print(movie.hasPrefix("A day"))
print(quote.hasSuffix(".jgp"))
```

[String Documentation](https://developer.apple.com/documentation/swift/string)

## 数字
### 整形Int

Swift的Int类型是8个Byte，也就是64个bit。所以Int类型的上下限非常大。
```swift
print(Int.max) // 9223372036854775807
print(Int.min) // -9223372036854775808
```

Swift的Int字面值可以用任意的`_`分隔，提供可读性。
```swift
let bigNumber = 1_000_000_000
let bigNumber = 10_0000_0000
let bigNumber = 1__00_000000____0
```

整形的方法
```swift
print(120.isMultiple(of: 3))
print(Int.random(in: 1..<100))
```
[Int Documentation](https://developer.apple.com/documentation/swift/int)

### 浮点数Double
Swift的Double和Int在计算时不会自动进行类型转换

```swift
let a = 1
let b = 0.1
c = a + b // ❌ error
c = Double(a) + b // 1.1
```
[Double Documentation](https://developer.apple.com/documentation/swift/double)