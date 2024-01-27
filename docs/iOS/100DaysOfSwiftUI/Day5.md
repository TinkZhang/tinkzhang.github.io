---
layout: default
title: Day 5 - 条件
parent: 100天学会SwiftUI
grand_parent: iOS
---

# 第五天：条件

<https://www.hackingwithswift.com/100/swiftui/5>

## If

```swift
if someCondition {
    print("Do something")
}
```

Swift的`if`后面没有()；

Swift的`if`是expression，是有值的，但是必须有'else'，保证条件的完备性。
```swift
let result = if statusCode == 200 {
    "success"
} else {
    "fail"
}
print(result)
```

## Switch-Case

```swift
switch forecast {
case .sun:
    print("It should be a nice day.")
case .rain:
    print("Pack an umbrella.")
case .wind:
    print("Wear something warm")
case .snow:
    print("School is cancelled.")
case .unknown:
    print("Our forecast generator is broken!")
default:
    print("...")
}
```

switch 后面也是不加括号的；可以通过default提供默认情况；switch也是expression。 

## 三目运算符

```swift
let age = 18
let canVote = age >= 18 ? "Yes" : "No"
```