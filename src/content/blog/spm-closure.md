---
title: Closure SPM
author: 0xLeif
pubDatetime:  2021-12-1T20:22:00Z
postSlug: my-recent-2
featured: false
draft: false
tags:
  - swift
  - spm
  - SwiftPackageManager
description:
    Define and chain Closures with Inputs and Outputs
---

# Closure SPM 📦

🔗 [_Check out Closure_](https://github.com/0xLeif/Closure)

<br/>

```shell
git clone git@github.com:0xLeif/Closure.git
```

<br/>

## Defining a Closure

_"A Closure is a block of code that can be executed by reference of a variable or name. Closures in Swift are normally unnamed and passed in as a parameter variable or stored as a variable."_

🔗 [source](/posts/swiftlet-05-closures/)

<br/>
<br/>

### Closure.swift

<br/>

When we define a Closure we can assume that it will always have an `Input` and an `Output`. Either value could be `Void` in the case that a value doesn't exist. Knowing this we can expect that our object look something like, `Closure<Input, Output>`. We will need an actual closure when we initialize our `Closure` object. This value should look something like this, `(Input) -> Output`.

<br/>

```swift
/// A Struct that defines a Closure with a given Input and a given Output
public struct Closure<Input, Output> {
  /// The Closure passed in during initialization
  public let method: (Input) -> Output
  
  /// Initialize a Closure without any scoped state
  public init(
    _ closure: @escaping (Input) -> Output
  ) {
    method = closure
  }
}
```

Notice that we must specify that the closure is `@escaping`. This is becuase we will store it in a variable that we can keep for the lifetime of the object. In other words `@escaping` means that the closure can leave the scope of the function it is passed into. 

<br/>
<br/>

### Running the Closure

<br/>

Now that we have defined the basic `Closure` object we can start running the closure! Currently we would need to reach into the object. You will also notice that we need to pass in `()` which is the Void type. 

<br/>

```swift
let sayHello = Closure {
    print("Hello 👋")
}

sayHello.method(())
```

_In this example, `sayHello` is of type `Closure<Void, Void>`._

<br/>
<br/>

### Extending Closure

<br/>

Now we will create a function to run the `Closure` with the required `Input` and potentially a completion handler. This will make it easier to call the method instead of having to reach into the object.

<br/>

```swift
public extension Closure {
  /// Run the Closure with Input and a Completion Handler
  func run(
    input: Input,
    onCompletion onCompletionHandler: () -> Void = {}
  ) -> Output {
    defer {
      onCompletionHandler()
    }
    return method(input)
  }
}
```

<br/>
<br/>

#### Void Input Closures

<br/>

Now that we have a run function, we can add another extension for when the `Input` is `Void`. We will add another run function where it doesn't require an `Input` and defaults the value to `()`.

<br/>

```swift
extension Closure where Input == Void {
    func run(
        onCompletion onCompletionHandler: () -> Void = {}
    ) -> Output {
        run(
            input: (),
            onCompletion: onCompletionHandler
        )
    }
}
```

<br/>
<br/>

#### Chaining Closures

<br/>

To be able to chain closures, we would need to receive some new closure to run. We can expect that this closure will look very similar to the closure we already have, but it could have some new output. The closure should look similar to this, `@escaping (Output) -> NewOutput`.

<br/>

```swift
extension Closure {
  /// Chain another Closure with a NewOutput
  func then<NewOutput>(
    _ closure: @escaping (Output) -> NewOutput
  ) -> Closure<Input, NewOutput> {
    Closure<Input, NewOutput> { input in
      closure(method(input))
    }
  }
}
```

Looking at this function, note that we pass the `Output` of `method(input)` into the new closure. Using `then`, we are able to make a new `Closure` where we still pass in the same type of `Input`, but now the `NewOutput` could be the same or different than `Output`.

<br/>

**Chaining Closures Example**

<br/>

Psuedo Code

`Closure<Void, Void> -> Closure<Void, Int> -> Closure<Void, Void>`

<br/>

```swift
let sayHello: Closure<Void, Void> = Closure {
    print("Hello")
}
.then {
    Int.random(in: 0 ... 9)
}
.then { randomInt in
    print("I got this random int: \(randomInt) 🤷‍♂️")
}
```

_In this example, `sayHello` is still of type `Closure<Void, Void>`._

<br/>
<br/>

## Stateful Closure

<br/>

🤔 _What is a stateful closure?_

<br/>

Could we have a Closure that has some state? For example, could we have a closure that returns a value and each time we run it it increments one to the value.

<br/>

```swift
let statefulCount: Closure<Void, Int> = ...

for _ in 0 ... 9 {
    print(statefulCount.run())
}

/** Output
0
1
2
3
4
5
6
7
8
9
*/
```

<br/>

To do this we need a new init!

<br/>

```swift
public struct Closure<Input, Output> {
    // ...
    
    /// Initialize a Closure with potential scoped state
    public init(
        _ closure: () -> ((Input) -> Output)
    ) {
        method = closure()
    }
}
```

<br/>

- In the example above where we have `statefulCount`. The `Closure` was defined with the following code.

<br/>

```swift
let statefulCount: Closure<Void, Int> = Closure {
    var count = 0
    
    return { _ in
        defer {
            count += 1
        }
        
        return count
    }
}
```

<br/>
<br/>

***

<br/>
<br/>

**Extra Examples**

<br/>

**No State**

```swift
let noStateCount = Closure<String, String> { text in
  String(repeating: text, count: 4)
}
.then { string in
  Int(string) ?? 0
}


XCTAssertEqual(noStateCount.method("5"), 5555)
XCTAssertEqual(noStateCount.method("5"), 5555)
XCTAssertEqual(noStateCount.method("5"), 5555)
```

<br/>

**State**

```swift
let stateCount: Closure<String, Int> = Closure<String, String> {
  var count = 1
  
  return { text in
    defer {
      count += 1
    }
    
    return String(repeating: text, count: count)
  }
}
.then { string in
  Int(string) ?? 0
}

XCTAssertEqual(stateCount.method("5"), 5)
XCTAssertEqual(stateCount.method("5"), 55)
XCTAssertEqual(stateCount.method("5"), 555)
```

⬆️ [Back to the Top](/posts/spm-closure/)
