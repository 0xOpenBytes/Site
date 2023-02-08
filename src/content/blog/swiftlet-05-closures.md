---
title: "SwiftLet 05: Closures"
author: 0xLeif
pubDatetime: 2022-06-06T04:06:31Z
postSlug: swiftlet-05-closures
featured: false
draft: false
tags:
  - swiftlet
  - swift
  - closures
description:
  A Closure is a block of code that can be executed by reference of a variable or name. Jump in and learn more about closures and how they can be used.
---

# SwiftLet #05: Closures
_Input and Output_

A Closure is a block of code that can be executed by reference of a variable or name. Closures in Swift are normally unnamed and passed in as a parameter variable or stored as a variable. Functions are named blocks of code, they can also be passed in as a parameter for a Closure type.

**Closure Type**
The most basic Closure type you can have is one that doesn’t take any parameter variables (input) and doesn’t return (output) anything. This Closure type is common and is know as the Void to Void closure.
```swift
let closure: () -> Void
```

The type of this closure denotes that it doesn’t take any parameters, `()`, and returns `Void` which every Closure in Swift, which doesn’t return a specified type, happens to return `Void`. 

Another example for a Closure type could be one that takes in some `Int` and returns some `String`.
```swift
let closure: (Int) -> String

closure = { times in
    String(repeating: "🧱", count: times)
}

func function(times: Int) -> String {
    String(repeating: "🧱", count: times)
}

print(closure(3)) // 🧱🧱🧱
print(function(times: 3)) // 🧱🧱🧱
```

Notice that the function has the same Closure type except that it has a named parameter `(times: Int) -> String`.  To show this we can have another function that has a parameter of `(Int) -> String`.
```swift
let closure: (Int) -> String

closure = { times in
    String(repeating: "🧱", count: times)
}

func function(times: Int) -> String {
    String(repeating: "🧱", count: times)
}

func task(closure: (Int) -> String) {
    print(closure(5))
}

task(closure: closure) // 🧱🧱🧱🧱🧱
task(closure: function) // 🧱🧱🧱🧱🧱
```
