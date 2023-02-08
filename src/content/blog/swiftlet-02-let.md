---
title: "SwiftLet #02 - Let"
author: 0xLeif
pubDatetime: 2021-11-30T17:26:00Z
postSlug: swiftlet-02-let
featured: false
draft: false
tags:
  - swiftlet
  - swift
description:
  Let us learn more about the let in this episode of SwiftLet!
---

# SwiftLet #02: Let

_Let is the keyword to define a variable that can only be set once._

```swift
let variable: String

variable = "👋"

// variable = "🙅" // This will result in a compiler error!
```

If you uncomment the line where `variable` is being set to 🙅, you will get a compiler error. 

`Immutable value 'variable' may only be initialized once`

**NOTE:** _It says initialized_

**Example 1**
Simply set the value. Go type inference!
```swift
let pi = Float.pi
```

**Example 2**
What if we tried to modify the value? In this example, we are trying to modify an Array after it has been initialized, in Swift Arrays are **Value Types** _(in a later chapter we will dive into the topic of **Value Types** and **Reference Types**)_.
```swift
let variable: [String]

variable = ["👋"]

variable.append("🙅") // This will also result in a compiler error!
```

The error you get is because **Value Types** are always reinitialized! Their value changed, so it is a **new** value.

`Mutating method 'append' may not be used on immutable value 'variable'`

**Example 3**
We can **get** the variable and use the value, in this example we print the current value to the console.
```swift
let variable = "👋"

print(variable) // 👋
```

**Closing Remarks**

We learned that `let` can only **set** a variable’s value once! Also we learned that we can **get** the value of a variable and use it. Finally we learned that Swift has **Value Types** and **Reference Types**; also that you can not modify a variable which happens to be a **Value Type**.
