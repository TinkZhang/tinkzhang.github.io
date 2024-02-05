---
layout: default
title: Day 11 - 结构体 属性访问性控制和静态属性方法
parent: 100天学会SwiftUI
grand_parent: iOS
---

# 第十一天：结构体 属性访问性控制和静态属性方法

<https://www.hackingwithswift.com/100/swiftui/11>

## 结构体的属性访问性控制

* private: 只能在当前的结构体访问
* fileprivate: 只能在当前的源文件中访问
* internal: 可以在当前的模块中访问
* public: 可以在任何地方访问

## 结构体的静态属性方法

```swift
struct School {
    static var studentCount = 0

    static func add(student: String) {
        print("\(student) joined the school.")
        studentCount += 1
    }
}
```

为了测试，一些数据结构体会定义一个example属性

```swift
struct Employee {
    let username: String
    let password: String

    static let example = Employee(username: "cfederighi", password: "hairforceone")
}
```