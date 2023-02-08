---
title: "SwiftLet #03: The var Variable"
author: 0xLeif
pubDatetime: 2022-06-06T04:06:31Z
postSlug: swiftlet-03-var
featured: false
draft: false
tags:
  - swift
  - swiftlet
description:
  Variables are used in every single Swift project and are important things! They do a variety of work for us so take a peek and learn all about them.
---

# SwiftLet #03: Var
_Var is the keyword to define a variable._

```swift
var variable: String

variable = "👋"

print(variable) // 👋

variable = "😱"

print(variable) // 😱
```

**Example 1**

Some types allow for the use of different operators! So far we have only used the assignment operator (**=**). For this example we will try using the addition operator (**+**). 

```swift
var variable: String

variable = "👋"

print(variable) // 👋

variable = variable + "😱"

print(variable) // 👋😱
```

**Example 2**

```swift
var variable: [String]

variable = ["👋"]

print(variable) // ["👋"]

variable.append("🤪")

print(variable) // ["👋", "🤪"]
```
