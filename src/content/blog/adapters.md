---
title: Adapt and Overcome! 
author: Rob Maltese
pubDatetime: 2023-02-08T03:06:31Z
postSlug: adapters
featured: true
draft: false
tags:
  - swift
  - swiftui
  - ios
description:
  Adapters make it easy for us to transform and mold network models into client models.
---

When working with JSON data, I often struggled with how to handle the data coming in, and how to mold that data into something I could use on the client side of things. When building out [iOS-base](https://github.com/0xOpenBytes/ios-base), it was apparent that we would want to create a simple, and reusable method that would be able to transform our data bi-directionally.

```swift
protocol Adaptable {
    associatedtype NetworkModel
    associatedtype DeviceModel

    static func device(from: NetworkModel) throws -> DeviceModel
}

protocol BiDirectionallyAdaptable: Adaptable {
    associatedtype NetworkModel
    associatedtype DeviceModel

    static func network(from: DeviceModel) throws -> NetworkModel
}
```

The two protocols shown above, are our Adapters. As you can see one takes in our NetworkModel and then returns that into our DeviceModel which is our client-side model. Additionally, the other protocol handles the reverse. It takes in the DeviceModel and then returns our NetworkModel. This is especially helpful when making POST requests.

### So how do we use it?

```swift
struct NetworkModel: Codable {
 let id: UUID
 let User_name: String
 let email_address: String
 let startTime: Date
} 
```

<br/>

Let's say that we have been given the task of fetching some JSON data, and that data doesn't have pretty or consistent naming. We will need our NetworkModel to conform to the JSON data to not run into decoding issues. As you can see above, we've got mixed cases and I don't personally want to use the same naming conventions on the client side. 

### Enter our adapter...

We first will define our client model which will have whatever naming convention I choose, and ideally it would be whatever that JSON object item is to the client.

```swift
struct DeviceModel: Codable {
  let id: UUID
  let username: String
  let email: String
  let jobStart: Date
} 
```

Now we will create the following adapter enum that will have our static function which we will later call on within our network layer or logic handling file.

```swift
enum UserAdapter: Adaptable {
  static func device(from: NetworkModel) throws -> DeviceModel {
    DeviceModel(
      id: from.id
      username: from.User_name
      email: from.emailAddress
      jobStart: from.startTime
  } 
}
```

As you can see, we’re taking in our NetworkModel and then returning and adapting to conform to our DeviceModel. This now allows us to use our adapter within our network layer to then use our DeviceModel on the View. 

```swift
func getUserData() async throws -> DeviceModel {
   let response: NetworkModel = try await fetchUser()
   return try UserAdapter.device(from: response)
}
```

Now as I like to say... bingo bongo! We've got ourselves a clean and easy way to convert our NetworkModel over to our DeviceModel after we return our data to the NetworkModel on the networking fetching layer. I will show more of that networking layering in another article as for this one, I wanted to try to keep it short and sweet.

