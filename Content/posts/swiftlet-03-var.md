---
date: 2021-11-30 17:26
description: SwiftLet #03
tags: swift, swiftlet
---
# SwiftLet #03: Var
_Var is the keyword to define a variable._

```swift
var variable: String

variable = "ð"

print(variable) // ð

variable = "ðą"

print(variable) // ðą
```

**Example 1**

Some types allow for the use of different operators! So far we have only used the assignment operator (**=**). For this example we will try using the addition operator (**+**). 

```swift
var variable: String

variable = "ð"

print(variable) // ð

variable = variable + "ðą"

print(variable) // ððą
```

**Example 2**

```swift
var variable: [String]

variable = ["ð"]

print(variable) // ["ð"]

variable.append("ðĪŠ")

print(variable) // ["ð", "ðĪŠ"]
```
