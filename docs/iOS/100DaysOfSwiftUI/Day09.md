---
layout: default
title: Day 09 - 闭包
parent: 100天学会SwiftUI
grand_parent: iOS
---

# 第九天：闭包
<https://www.hackingwithswift.com/100/swiftui/9>

```swift
let sayHello = { (name: String) -> String in
    "Hi \(name)!"
}
```

这个sayHello的类型是`(String) -> String`。

```swift
let team = ["Gloria", "Suzanne", "Piper", "Tiffany", "Tasha"]

let captainFirstTeam = team.sorted(by: { (name1: String, name2: String) -> Bool in
    if name1 == "Suzanne" {
        return true
    } else if name2 == "Suzanne" {
        return false
    }

    return name1 < name2
})

print(captainFirstTeam)

// 因为sorted函数的参数是闭包，且函数定义的时候已知闭包的类型，所以可以省略
let captainFirstTeam = team.sorted { name1, name2 in
    if name1 == "Suzanne" {
        return true
    } else if name2 == "Suzanne" {
        return false
    }

    return name1 < name2
}

// 可以进一步省略
let captainFirstTeam = team.sorted {
    if $0 == "Suzanne" {
        return true
    } else if $1 == "Suzanne" {
        return false
    }

    return $0 < $1
}
```

一些集合函数，经常可以使用`$0`，`$1`，`$2`来代表闭包的参数。
```swift
let uppercaseTeam = team.map { $0.uppercased() }
print(uppercaseTeam)
``
