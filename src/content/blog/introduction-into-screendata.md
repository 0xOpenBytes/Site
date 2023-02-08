---
author: 0xLeif
pubDatetime: 2021-11-30T17:26:00Z
title: Introduction into ScreenData in 2021
postSlug: introduction-into-screendata
featured: false
draft: false
tags:
  - swift
  - screendata
  - ios
  - swiftui
ogImage: ""
description:
  Introduction into the use of ScreenData in 2021.
---

# An Intro into ScreenData in 2021

<br/>

[ScreenData](https://github.com/ServerDriven/ScreenData) is a data model for displaying UI Screens.  A **Screen** is what contains all the views for ScreenData.  **Screens** have **Views** which contain all the information they need to be displayed to the screen. **ContainerViews** can have multiple **Views** and specify a axis, horizontal or vertical, which the **Views** are aligned on. **Views** can have destinations which link to another **Screen**.

<br/>

Since ScreenData is a data model, any programming language can implement it! Currently there are two implementations of ScreenData, [Kotlin](https://github.com/ServerDriven/ScreenData-kotlin) and [Swift](https://github.com/ServerDriven/ScreenData-swift).  Official ScreenData repositories have been created for [Typescript](https://github.com/ServerDriven/ScreenData-typescript), [Rust](https://github.com/ServerDriven/ScreenData-rust), and [Dart](https://github.com/ServerDriven/ScreenData-dart). All are open for anyone to implement.

<br/>

After you have chosen your preferred ScreenData implementation, you can start deciding how you will get some **Screen** and optionally store it.  For instance here are some examples.

<br/>

- Storing the ScreenData or JSON locally to be able to fetch it instantly
- Fetching the data from a server
- Fetch the data from a server, but then cache a local version of the data until some indeterminate time in the future

<br/>

## ScreenDataUI and CustomView

<br/>

All of these decisions are influenced by what ScreenDataUI implementation you choose.  Currently there are two implementations of ScreenDataUI, [iOS (SwiftUI)](https://github.com/ServerDriven/ScreenDataUI-ios) and [Android (Compose)](https://github.com/ServerDriven/ScreenDataUI-android).  These implementations are intended to be a 1:1 implementation of ScreenData for mobile. Not all implementations use everything that ScreenData has to offer. If you find ScreenData doesn’t have what you need, you can always use a **CustomView**. When using a **CustomView**, the front end will need to have its own implementation of the view. **CustomViews** should use an id so that the front end can tell what to display. 
