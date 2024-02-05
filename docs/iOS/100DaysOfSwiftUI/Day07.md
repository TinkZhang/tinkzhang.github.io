---
layout: default
title: Day 07 - 函数定义和参数名
parent: 100天学会SwiftUI
grand_parent: iOS
---

# 第七天：函数定义和参数名

<https://www.hackingwithswift.com/100/swiftui/7>

```swift
func greeting(name: String) {
    print("Hello \(name).")
}

greeting(name: "Tink")

func rollDice() -> Int {
    Int.random(in: 1...6)
}
```

- 关键字`func`
- 调用函数的时候需要参数名

## 返回值

如果函数体中只有一个表达式，可以省略`return`

```swift
func greet(name: String) -> String {
    if name == "Taylor Swift" {
        "Oh wow!"
    } else {
        "Hello, \(name)"
    }
}
```

可以利用`tuple`返回多个值

```swift
func getUser() -> (firstName: String, lastName: String) {
    (firstName: "Taylor", lastName: "Swift")
}

// 可以省去名字
func getUser() -> (String, String) {
    ("Taylor", "Swift")
}

// 如果只要部分返回信息
let (firstName, _) = getUser()
print("Name: \(firstName)")
```

## 参数名

默认 Swift 函数是必须要有参数名的。如果我们调用函数不想参数名，定义函数的时候可以用`_`

```swift
func isUppercase(_ string: String) -> Bool {
    string == string.uppercased()
}
isUppercase("HE")
```

另一种情况是为了提高代码的可读性，函数定义一个内部参数名和外部参数名。

```swift
func printTimesTables(for number: Int) {
    for i in 1...12 {
        print("\(i) x \(number) is \(i * number)")
    }
}
printTimesTables(for: 5)
```
