---
title: "SwiftLet 04: Optionals"
author: 0xLeif
pubDatetime: 2021-11-30T04:06:31Z
postSlug: swiftlet-04-optionals
featured: false
draft: false
tags:
  - swift
  - swiftlet
  - optionals
description: What if a variable doesn't always need to have a variable? Well, that means it's an optional!
---

# SwiftLet #04: Optionals

_What if a variable shouldn’t have a value?_

Great question! Luckily Swift has what are known as Optionals. Optionals **optionally** have a value! Let’s say we have a variable that is the name of our favorite ice cream.

```swift
var favoriteIceCreamFlavor: String
```

Well let’s say we have a friend that hates ice cream, they don’t even have a least favorite flavor! You may think, wait can’t we just put nothing as the string?

```swift
favoriteIceCreamFlavor = ""
```

Sure! Although this could cause issues, why isn’t the `favoriteIceCreamFlavor` just **n/a**? In Swift `nil` is the value denoted to mean nothing or does not exist.

This is when we want to use optionals! Now we can print out the `favoriteIceCreamFlavor` and it will print out `nil`.

```swift
var favoriteIceCreamFlavor: String?

print(favoriteIceCreamFlavor) // nil
```

Although now, when we set the `favoriteIceCreamFlavor` to some flavor and print it out we get some different output than if we used just a `String` and not an `String?` (optional string).

```swift
var favoriteIceCreamFlavor: String?

favoriteIceCreamFlavor = "Coffee"

print(favoriteIceCreamFlavor) // Optional("Coffee")
```

For some reason we are getting our favorite ice cream flavor, but it is being wrapped with `Optional`. In Swift Optionals help us deal with variables that may not always have a value. If we wanted to print out `favoriteIceCreamFlavor` as a `String` and not a `String?`, we just need to unwrap the value! Swift has a few different ways to unwrap an Optional, the first we will discuss is the one you should **almost never use**!

**Force Unwrap**
When you force unwrap an Optional in Swift it will return the unwrapped value or crash your program! **Be careful!**

```swift
var favoriteIceCreamFlavor: String?

favoriteIceCreamFlavor = "Coffee"

print(favoriteIceCreamFlavor!) // Coffee
```

If we didn’t have a `favoriteIceCreamFlavor` set our app would crash and give us an error.

```swift
var favoriteIceCreamFlavor: String?

print(favoriteIceCreamFlavor!)
// Fatal error: Unexpectedly found nil while unwrapping an Optional value
// Terminated due to signal: ILLEGAL INSTRUCTION (4)
```

**Default Unwrap**
Instead of force unwrapping, there is always the option to provide a default value if the variable is `nil`!

```swift
var favoriteIceCreamFlavor: String?

favoriteIceCreamFlavor = "Coffee"

print(favoriteIceCreamFlavor ?? "N/A") // Coffee
```

If the variable is `nil` it will just default to the value we provided.

```swift
var favoriteIceCreamFlavor: String?

print(favoriteIceCreamFlavor ?? "N/A") // N/A
```

**Conditionally Unwrap**
Swift also can unwrap Optionals using an `if` or `guard` statement. Simply initialize a new variable inside the conditional statement.

**if let**

```swift
var favoriteIceCreamFlavor: String? = Bool.random() ? "Coffee" : nil

if let unwrappedFavoriteIceCreamFlavor = favoriteIceCreamFlavor {
    print(unwrappedFavoriteIceCreamFlavor)
} else {
    print(unwrappedFavoriteIceCreamFlavor) // Error: Cannot find 'unwrappedFavoriteIceCreamFlavor' in scope
    print("None!")
}
```

This example will randomly set the value of `favoriteIceCreamFlavor` to “Coffee“ or `nil`. Then it will only print the ice cream flavor if it is not `nil`. Otherwise it will just print “None!”. Notice that `unwrappedFavoriteIceCreamFlavor` is a new variable and is only usage within the scope of the statement it belongs to.

```swift
var favoriteIceCreamFlavor: String? = Bool.random() ? "Coffee" : nil

if let unwrappedFavoriteIceCreamFlavor = favoriteIceCreamFlavor,
    unwrappedFavoriteIceCreamFlavor == "Coffee" {
    print(unwrappedFavoriteIceCreamFlavor)
} else if var unwrappedFavoriteIceCreamFlavor = favoriteIceCreamFlavor {
    unwrappedFavoriteIceCreamFlavor = "Coffee"
    print(unwrappedFavoriteIceCreamFlavor)
} else {
    print("None!")
}
```

You can even specify that the locally unwrapped variable is mutable! Which doesn’t change the original `favoriteIceCreamFlavor` if that variable is a Value Type. If the variable is a Reference Type, it can modify any variable that is a `var` and you have access to.

**guard let**

```swift
var favoriteIceCreamFlavor: String? = Bool.random() ? "Coffee" : nil

guard let unwrappedFavoriteIceCreamFlavor = favoriteIceCreamFlavor else {
//    print(unwrappedFavoriteIceCreamFlavor) // Error: Cannot find 'unwrappedFavoriteIceCreamFlavor' in scope
    print("None!")
    return
}

print(unwrappedFavoriteIceCreamFlavor)
```
