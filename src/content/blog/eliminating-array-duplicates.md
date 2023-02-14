---
title: Eliminating Duplicates in Arrays
author: Rob Maltese
pubDatetime: 2022-02-13T18:34:31Z
postSlug: eliminating-duplicates-in-arrays
featured: false
draft: false
tags:
  - swift
  - swiftui
  - array
description:
  While working with arrays, you may be tasked in making sure said array does not have any duplicates. We'll cover a few various methods to complete that within this article.
---

Arrays are an ordered random access collection in which contains elements of a defined data type. These types can be anything from an `Int` to a defined model. An array is something that you will see very often within Swift projects when organizing your apps data. The downfall to an array is that these items are not unique and the collection may contain duplicates.

### Array Example
```swift
let numbers = [1, 3, 3, 5, 4, 4]
let names = ["Billy", "Sam", "Emily", "Bob", "Sam", "Billy"]
```

Lets check out the methods we can use to eliminate the duplicates in the arrays above.

## Using Swift Algorithms

At [WWDC 2021](https://developer.apple.com/videos/play/wwdc2021/10256/), Apple announced two new open source frameworks, one of them being [Swift Algorithms](https://github.com/apple/swift-algorithms). This is a stand-alone package that can be added to your project. Within the Swift Algorithm package contains a method called `.uniqued()` which removes duplicates from your array. 

The only requirement to using this method, and much of Swift Algorithms is that your array elements must conform to `Hashable`. After adding the package to your project, you will simply use it in the following manner.

```swift
import Algorithms

let numbers = [1, 3, 3, 5, 4, 4,]
let uniquedNumbers = numbers.uniqued()

let names = ["Billy", "Sam", "Emily", "Bob", "Sam", "Billy"]
let uniquedNames = names.uniqued()
```

This will return `uniquedNumbers` as a `UniquedSequence` which conforms to `LazySequenceProtocol`. You can then call that variable wherever you would call your array.

## Using Array Extension

I often times don't like adding dependencies unless absolutely needed. When adding them, I always way out the pros and cons, and if I can do it myself - I will. This method eliminates the need for the dependency and uses an array extension to filter the array and remove the duplicates. It will return a new array, without the duplicates.

```swift
extension Array where Element: Hashable {
    func removingDuplicates() -> [Element] {
        var addedDict = [Element: Bool]()

        return filter {
            addedDict.updateValue(true, forKey: $0) == nil
        }
    }

    mutating func removeDuplicates() {
        self = self.removingDuplicates()
    }
}
```

Then to use the above extension, we'll simply call the function on an array, much like we would do in the Swift Algorithms example.

```swift
let numbers = [1, 3, 3, 5, 4, 4,]
let uniquedNumbers = numbers.removingDuplicates()

let names = ["Billy", "Sam", "Emily", "Bob", "Sam", "Billy"]
let uniquedNames = names.removingDuplicates()
```


