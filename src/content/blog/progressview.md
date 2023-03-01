---
title: Improving UX Using ProgressView
author: Rob Maltese
pubDatetime: 2023-02-18T15:06:31Z
postSlug: improving-ux-with-processview
featured: false
draft: false
tags:
  - swiftui
  - swift
  - ios
  - user-experience
description: Your users experience is important, and it's better to show something than nothing. Using SwiftUI ProgressView does just that.
---

The users experience is extremely important, and in my opinion there's nothing worse then trying to interact with what seems like a frozen application. So what can we do to fix that awkward stage between displaying content to our users, and the loading state while our application is processing our requests? Progress indicators!

<img src="/public/assets/posts/images/progressview/loadingimage.jpg" alt="Loading image from Unsplash." width="50%"/>

## We're working here!

Progress indicators help your users know that your app hasn't stalled out, rather it is in a loading state working behind the scenes while it performs some sort of operation. There are two types of progress indicators that we can use, and it is based on whether or not we know the duration of an operation.

- _Determinate_, used with tasks with a well-defined duration.
- _Indeterminate_, for unquantifiable tasks such as loading or syncing data.

Thankfully SwiftUI provides us with a few handy progress indicators to help us display progress indicators and loading states to our users.

## Just the basics

The most simple, and basic way to display a simple loading indicator to let your users know you're loading something is with `ProgressView()`. It doesn't get much easier then that!

```swift
struct ContentView: View {
  var body: some View {
    ProgressView()
  }
}
```

The above code displays a clean and simple loading spinner.
<img src="/assets/posts/images/progressview/progressviewspinner.gif" alt="Basic SwiftUI ProgressView spinner." width="35%"/>

## Lets get linear

We can add a little bit of flair by changing the default `ProgressView()` style to `LinearProgressViewStyle()` by adding the value parameter which accepts a `Float`.

```swift
struct ContentView: View {
  var body: some View {
    ProgressView(value: 1.0)
  }
}
```

<img src="/assets/posts/images/progressview/linearprogressview.gif" alt="Basic SwiftUI ProgressView linear example." width="35%"/>

This code will display a filled linear progress view. Animating the view on change appeared a bit tricky to me, so I did what any good developer does... Googles the crap out of an issue and lands on <a href="https://stackoverflow.com/a/67135277/14128044">Stack Overflow.</a> to fix the problem. A bit of that code, leads us to this beautiful animated linear progress view.

## When should I use ProgressView?

Real life examples are the best learning tool, and recently I had the chance to learn that lesson. In this view, a user is displayed the current response time for the servers however, while the data is loading I unfortunately am showing `-99` which is my optional string return. What should be showed here is progress view spinners rather then what is.

<img src="/assets/posts/images/progressview/spinnerexample.png" alt="Image showing a vertical line of progress view spinners"/>

## Apple recommended best practices? Say what!?

- **When possible, use a determinate progress indicator.** An indeterminate progress indicator shows that a process is occurring, but it doesn’t help people estimate how long a task will take. A determinate progress indicator can help people decide whether to do something else while waiting for the task to complete, restart the task at a different time, or abandon the task.
- **Be as accurate as possible when reporting advancement in a determinate progress indicator.** Consider evening out the pace of advancement to help people feel confident about the time needed for the task to complete. Showing 90 percent completion in five seconds and the last 10 percent in 5 minutes can make people wonder if your app is still working and can even feel deceptive.
- **Keep progress indicators moving so people know something is continuing to happen.** People tend to associate a stationary indicator with a stalled process or a frozen app. If a process stalls for some reason, provide feedback that helps people understand the problem and what they can do about it.
- **When possible, switch a progress bar from indeterminate to determinate.** If an indeterminate process reaches a point where you can determine its duration, switch to a determinate progress bar. People generally prefer a determinate progress indicator, because it helps them gauge what’s happening and how long it will take.
- **Don’t switch from the circular style to the bar style.** Spinners and progress bars are different shapes and sizes, so transitioning between them can disrupt your interface and confuse people.
- **If it’s helpful, display a description that provides additional context for the task.** Be accurate and succinct. Avoid vague terms like loading or authenticating because they seldom add value.
- **Display a progress indicator in a consistent location.** Choosing a consistent location for a progress indicator helps people reliably find the status of an operation across platforms or within or between apps.
- **When it’s feasible, let people halt processing.** If people can interrupt a process without causing negative side effects, include a Cancel button. If interrupting the process might cause negative side effects — such as losing the downloaded portion of a file — it can be useful to provide a Pause button in addition to a Cancel button.
- **Let people know when halting a process has a negative consequence.** When canceling a process results in lost progress, it’s helpful to provide an alert with an an option to confirm the cancellation or resume the process.

The best place to learn about user experience, is the <a href="https://developer.apple.com/design/human-interface-guidelines/components/status/progress-indicators/">Apple Human Interface Guidelines</a>.
