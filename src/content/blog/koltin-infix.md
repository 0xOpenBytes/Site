---
title: Koltin infix Notation
author: Parshav
pubDatetime: 2021-12-24T20:24:00
postSlug: koltin-infix-notation
featured: true
draft: false
tags:
  - koltin
  - android
description:
  Koltin infix keyword allows for calling without parenthesis.
---

# Kotlin infix notation

### What does it do

<br/>

The `infix` keyword can be applied to kotlin functions. This simply allows it to be called without requiring parenthesis for its parameter. 

<br/>

Here's a small example with a `Player` that can hold a `card` at any given time. The player can `swapCard` if the other card's value is greater than the one they hold. We apply the `infix`  notation to the `swapCard` function.

```kotlin
class Player(card: Card) {

    var card: Card = card
        private set

    infix fun swapCard(other: Card) {
        if (other.value > card.value) {
            card = other
        }
    }
    
    override fun toString(): String {
        return "Player Card :: ${card.value}"
    }
}

data class Card(val value: Int)

```

<br/>

Lets try swapping a players card

```kotlin
@Test
fun `test swap`() {
    val purplePlayer = Player(Card(4))

    purplePlayer swapCard Card(6)

    println(purplePlayer) // successful swap 
    // prints Player Card :: 6

    purplePlayer swapCard Card(5) //unsuccessful swap
    // prints Player Card :: 6

    println(purplePlayer)
}
```

<br/>

We're able to call the `swapCard` function without using the parenthesis.

<br/>

### Constriants

<br/>

Only a single parameter can be passed into them.

```kotlin
class Player (...) {
    ...
    infix fun swapTwo(other: Card, cardB: Card) { ... } // will NOT compile
    ...	
}
```

<br/>

### Usage in standard library

<br/>

Infix functions are already used within the standard Kotlin library as well. `until` returns a range from the provided lower and upper bound.

```kotlin
@Test
fun `range demonstration`() {
    (0 until 10).forEach {
        print(it)
    }
}
// prints 0123456789
``` 

<br/>

Another common usage is the `to` infix function when adding elements to a map.

```kotlin
@Test
fun `map to demonstration`() {
    val dummyMap = mapOf(
        "One" to 1,
        "Two" to 2
    )
    dummyMap.forEach { (k, v) ->
        print("$k $v ")
    }
}
// prints One 1 Two 2
```

