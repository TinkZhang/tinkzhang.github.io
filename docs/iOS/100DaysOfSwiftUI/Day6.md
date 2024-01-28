---
layout: default
title: Day 6 - 循环
parent: 100天学会SwiftUI
grand_parent: iOS
---

# 第六天：循环

<https://www.hackingwithswift.com/100/swiftui/6>

## for in

```swift
let platforms = ["iOS", "macOS", "tvOS", "watchOS"]

for os in platforms {
    print("Swift works great on \(os).")
}

for i in 1...12 {
    print("5 x \(i) is \(5 * i)")
}

for i in 1..<5 {
    print("Counting 1 up to 5: \(i)")
}

for _ in 1...5 {
    lyric += " hate"
}
```

`1...12`是包含1和12的`ClosedRange`，`1..<5`是不包含5的`Range`。

如果需要特定的`step`，使用`stride`函数。
```swift
for radians in stride(from: 0.0, to: .pi * 2, by: .pi / 2) {
    let degrees = Int(radians * 180 / .pi)
    print("Degrees: \(degrees), radians: \(radians)")
}
```

## while

```swift
var countdown = 10

while countdown > 0 {
    print("\(countdown)…")
    countdown -= 1
}
print("Blast off!")
```

## break & continue

`break`退出循环；`continue`跳过本次循环
