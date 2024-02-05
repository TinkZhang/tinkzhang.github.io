---
layout: default
title: Day 10 - 结构体1
parent: 100天学会SwiftUI
grand_parent: iOS
---

# 第十天：结构体1

<https://www.hackingwithswift.com/100/swiftui/10>

## 结构体的声明和使用

```swift
struct Album {
    let title: String
    let artist: String
    let year: Int

    func printSummary() {
        print("\(title) (\(year)) by \(artist)")
    }
}
let red = Album(title: "Red", artist: "Taylor Swift", year: 2012)
let wings = Album(title: "Wings", artist: "BTS", year: 2016)

print(red.title)
print(wings.artist)

red.printSummary()
wings.printSummary()
```

## 结构体的初始化

结构体默认有一个`init()`初始化函数，所以以下两种写法是一样的。
```swift
let a = Album(title: "Red", artist: "Taylor Swift", year: 2012)
let a = Album.init(title: "Wings", artist: "BTS", year: 2016)
```

如果结构体的属性有默认值，那么可以省略初始化过程。

```swift    
struct Album {
    let title: String
    let artist: String
    let year: Int = 2009

    func printSummary() {
        print("\(title) (\(year)) by \(artist)")
    }
}

Album(title: "Red", artist: "Taylor Swift")
Album(title: "Wings", artist: "BTS", year: 2016)
```

## 结构体的可变性

```swift
struct Employee {
    let name: String
    var vacationRemaining: Int

    func takeVacation(days: Int) {
        if vacationRemaining > days {
            vacationRemaining -= days
            print("I'm going on vacation!")
            print("Days remaining: \(vacationRemaining)")
        } else {
            print("Oops! There aren't enough days remaining.")
        }
    }
}
```

以上代码编译会失败，如果方法需要改变结构体的属性，那么必须在方法前面加上`mutating`关键字。

```swift
var archer = Employee(name: "Sterling Archer", vacationRemaining: 14)
archer.takeVacation(days: 5)
print(archer.vacationRemaining)
```
以上代码是可以正常运行的。
但是如果改成`let archer = ...`，就会报错。`mutating`方法只能用在变量上，不能用在常量上。

## 存储属性和计算属性

```swift
// 只读
var vacationRemaining: Int {
    vacationAllocated - vacationTaken
}

// 读写
var vacationRemaining: Int {
    get {
        vacationAllocated - vacationTaken
    }

    set {
        vacationAllocated = vacationTaken + newValue
    }
}
```

## 属性观察器
```swift
struct App {
    var contacts = [String]() {
        willSet {
            print("Current value is: \(contacts)")
            print("New value will be: \(newValue)")
        }

        didSet {
            print("There are now \(contacts.count) contacts.")
            print("Old value was \(oldValue)")
        }
    }
}
```

## 自定义构造过程

```swift
struct Player {
    let name: String
    let number: Int

    init(name: String) {
        self.name = name
        number = Int.random(in: 1...99)
    }
}

let player = Player(name: "Megan R")
print(player.number)
```

有了自定义构造器，默认的构造器就不再存在了。如果需要使用默认构造器，必须自己写一个。
构造结束后，所有属性都必须有值。