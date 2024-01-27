---
layout: default
title: Day 2: 布尔值，字符串连接
parent: 100天学会SwiftUI
grand_parent: iOS
---

# 第二天：布尔值，字符串连接

<https://www.hackingwithswift.com/100/swiftui/2>

## 布尔值

Swift中的布尔值字面量首字母是小写的。

```swift
var gameOver = false
gameOver.toggle()
```

## 字符串连接

### 使用加号（+）运算符。

```swift
let string1 = "hello"
let string2 = "world"
let welcome = string1 + string2

let luggageCode = "1" + "2" + "3" + "4" + "5"
```
每次字符串连接都会创建一个新的字符串，所以如果你需要拼接很多字符串，使用加号运算符会比较慢。

而且Swift不支持自动类型转换，所以下面这段代码是错误的。

```swift
let number = 1 
let missionMessage = "Apollo " + number + " landed on the moon." // ❌
```

### 使用字符串插值(string interpolation)

```swift
let number = 1 
let missionMessage = "Apollo \(number) landed on the moon." // ✅
```