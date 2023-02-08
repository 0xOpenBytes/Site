---
title: Reduce and Fold
author: Parshav
pubDatetime: 2021-12-20T12:00:00
postSlug: reduce-and-fold
featured: false
draft: false
tags:
  - koltin
  - android
description:
    An introduction to Kotlin's `reduce` and `fold` functions, along with some use cases.
---

<br/>

# Reduce and Fold

<br/>

`reduce` and `fold` are functions for `Iterable` types in Kotlin that are used for accumulating values.

A simple example where we add numbers from 0 till 4. Typically we would write something like 

<br/>

```kotlin
@Test
fun `without`() {
    val testList = (0 until 5).toList()
    var acc = 0
    testList.forEach {
        acc += it
    }
    println("acc :: $acc") // acc :: 10
}
```

<br/>

We maintain a variable `acc` that holds the accumulated value.

`reduce` and `fold` functions provide both an accumulated value, along with the current value for the loop. In the following example, `acc` and `i` are these values respectively. Once the iteration is complete, these functions return the final accumulated value.

<br/>

```kotlin
@Test
fun `simple demonstration`() {
    val testList = (0 until 5).toList()
    val fold = testList.fold(0) { acc, i ->
        acc + i
    }
    println("Fold :: $fold") // Fold :: 10
    val reduce = testList.reduce { acc, i ->
        acc + i
    }
    println("Reduce :: $reduce") // Reduce :: 10
}
```

<br/>

Similar, but only slightly.
<br/>

## Difference

<br/>

Looking at our example, `reduce` does not explicitly provide a parameter to pass an initial value like `fold` does. It automatically uses the first item of the iterable type as the initial value.

But why separate these two, and where would you use one over the other ?

`fold`'s initial value defines its return type, whereas `reduce` expects the accumulated value to remain of the same type as the iterable it is being applied to.

Let's say we wish to iterate over our `testList` containing the numbers 0 till 4, and simply return a string joining all these numbers. Using `fold` we could do something like

```kotlin
@Test
fun `types difference`() {
    val testList = (0 until 5).toList()

    val fold = testList.fold("") { acc, i ->
        acc.plus(i)
    }

    println(fold)
}
```

where we provide an empty initial string as the first "accumulated" value, and our lamda appends the next number to the string.

*Changing the return type would not be possible in `reduce`*

<br/>

## Use case


### reduce

<br/>

A user can add multiple items to their basket when shopping, and we wish to display a running total of the price of these items.

An item is defined as ::

```kotlin
data class Item(
    val id: Int,
    val name: String,
    val price: Int
)
```

<br/>

And to generate the price of items for a given list ::

```kotlin
@Test
fun `reduce use case`() {
    val items = listOf(
        Item(
            id = 0,
            name = "Orange",
            price = 4
        ),
        Item(
            id = 1,
            name = "Milk",
            price = 5
        ),
        Item(
            id = 2,
            name = "Expensive Potato",
            price = 15
        )
    )

    val totalPrice = items
        .map { it.price }
        .reduce { acc, i -> acc + i }

    println("Total Price :: $totalPrice") // prints Total Price :: 24
}
```

<br/>

### fold

<br/>

Before we send data to our API, we perform client side validation to rid of any basic missing information. The object is complex, so we've created separate validators, each with their own concern.

Our complex `user` model

```kotlin
data class UserModel(
    val id: Int,
    val name: String,
    val email: String,
    val zipCode: Int
)
```

<br/>

Our validators for a `user`

```kotlin
interface Validator {
    fun isValid(user: UserModel): Boolean
}

class EmailValidator : Validator {
    override fun isValid(user: UserModel): Boolean {
        return user.email.contains("@")
    }
}

class ZipCodeValidator : Validator {
    override fun isValid(user: UserModel): Boolean {
        return user.zipCode >= 10_000
    }
}
```

<br/>

And now lets run our validators on an invalid user

```kotlin
@Test
fun `fold use case`() {
    val validators = listOf(
        EmailValidator(),
        ZipCodeValidator()
    )
    val userInvalid = UserModel(
        id = 0,
        name = "Kahani",
        email = "kahani#me.com",
        zipCode = 23_13
    )

    val isUserValid = validators.fold(true) { acc, validator ->
        acc && validator.isValid(userInvalid)
    }
    println("UserValid :: $isUserValid") // prints UserValid :: false
}
```

The fold iterates through each iterator and flips to false if any validation check fails.

<br/>

## Extra bytes

<br/>

- **What if our Iterable is empty ?**

<br/>

In this case `reduce` will throw an exception as it does not know what to return, where as `fold` will simply return the initial value provided. The `reduceOrNull` function will return `null` if you run into a situation where it is unsure if the iterable will be empty or not.

<br/>
<br/>
	
- **What if we want the current index throughout the iteration ?**

<br/>

`reduceIndexed` and `foldIndexed` provide a third variable, the index, to the lamda.

<br/>
<br/>

-  **`runningReduce` and `runningFold`**

<br/>

These functions work similar to `reduce` and `fold`, however instead of returning the accumulated value, it returns a list of values accumulated over each loop. When I find a better use case for this, I'll expand on it!
