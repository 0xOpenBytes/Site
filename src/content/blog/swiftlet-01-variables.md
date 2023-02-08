---
title: "SwiftLet #01: Variables"
author: 0xLeif
pubDatetime: 2022-06-06T04:06:31Z
postSlug: swift-let-variables
featured: false
draft: false
tags:
  - swift
  - swiftui
  - swiftlet
description:
  "SwiftLet #01: Variables! In this article we dive into variables and their various (pun intended) usecases."
---

# SwiftLet #01: Variables
One can think of variables as a named value. The value of the variable could be anything: a number, some words, an image, etc. All variables need to be **set** before we can **get** the actual value.

`{Keyword} {Variable Name}(: {Type}) = ({Value})`

It is required to specify if the variable is constant or modifiable. If the variable is a constant, we will denote that with the keyword of `let` otherwise if the variable is modifiable, we will use `var`. After specifying if the variable is a constant or not, we need to give the variable a name! The name of the variable can be anything, in Swift it could even be an emoji! After the variable’s name, we have the option to specify the type of the value, but this is optional if you set the value on the same line. This is because of Swift’s type inference! Lastly we have the option of if we want to **set** the variable’s value now or later, but we **must set** the variable’s value before trying to **get** it.

**Example 1**
```swift
// Format: {Keyword} {Variable Name} = {Value}
let variable = "Hello, World!"
```

**Example 2**
```swift
// Format: {Keyword} {Variable Name}: {Type} = {Value}
let variable: String = "Hello, World!"
```

**Example 3**
```swift
// Format: {Keyword} {Variable Name}: {Type}
let variable: String

variable = "🥇"
```


**Basic Types**

```swift
let boolean: Bool = Bool.random() // true or false 
let integer: Int = Int.max // 9223372036854775807
let float: Float = Float.pi // 3.1415925
let double: Double = Double.pi // 3.141592653589793
let character: Character "S"
let string: String = "Hello, World!"
```

**Collection Types**

```swift
let array: [Int] = [0, 1, 2]
let dictionary: [String: Int] = ["single": 1]
let set: Set = Set([0, 1, 1, 2])
// let set: Set = [0, 1, 1, 2] // You can also just say an Array is a Set!
```

**The Any Type**
```swift
let boolean: Any = Bool.random() // true or false 
let integer: Any = Int.max // 9223372036854775807
let float: Any = Float.pi // 3.1415925
let double: Any = Double.pi // 3.141592653589793
let character: Any "S"
let string: Any = "Hello, World!" 
```
