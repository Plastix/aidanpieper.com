+++
title = "Beginning with Jetpack Compose (Beta)"
date = "2021-04-11"
description = "My thoughts on Android's Jetpack Compose beta UI toolkit"
tags = ["kotlin","android", "jetpack compose"]
+++

> **TL;DR** Compose is a pretty great UI framework and you should try it out. However, it still has some teething pains in beta!

I'll be the first to admit that I've been pretty slow to adopt many of the libraries in Android's first party [Jetpack suite](https://developer.android.com/jetpack). Today, I want to talk about my initial thoughts with [Jetpack Compose](https://developer.android.com/jetpack/compose), Android's new declaritve UI toolkit which went into Beta a few weeks ago.

I tend to approach all new technology with a healthy dose of skepticism and Jetpack Compose was no exception. I'm pretty competent with Android's current UI toolkit and I didn't think that Compose would be a big step forward. However, I was pleasently surprised with Jetpack Compose.

## :heart: The Good

**It feels like magic**:
I love not writing boring UI binding code. :heart_eyes:

**Simple things are really really easy**:
Once you get past the initial learning curve, small things are really quick. Simple layouts and buttons work well out of the box. Additionally, it is hard to believe that this is all the code required to implement a performant scrolling list:[^recyclerview]
```kotlin
LazyColumn(
    contentPadding = PaddingValues(16.dp),
    modifier = Modifier.fillMaxSize(),
    verticalArrangement = Arrangement.spacedBy(8.dp)
) {
    items(puzzles) { puzzle ->
        PuzzleRow(puzzle, onPuzzleClick)
    }
}
```

**IDE Previews**:
I barely used the old layout preview in Android Studio because it didn't work half the time, and when it did, it usually didn't render accurately. I've been pleasantly surprised with the Compose IDE preview tool. It makes it very easy to preview your UI with lots of varied test data. Although it takes a few seconds to compile your Compose file, it is still a lot faster than a full app incremental build. Aditionally, it is super cool to be able to individually deploy a single component to your device.[^ide-tooling]
![Sample IDE preview](/images/beginning-with-jetpack-compose-beta/ide_preview.png)

## :thumbsdown: The Bad

**Relearning everything**:
I think this goes without saying. At a semantic level, Compose does everything the old Android layout system does. However, you need to relearn every API. Many APIs translate in non-obvious ways. For example, padding is done via Compose's `Modifier` system but margins don't exist in Compose; You are supposed to use a `Spacer` UI element.

**Out of date docs and code samples**:
At the time of writing, Compose is currently in `Beta04`. However, a lot of APIs have changed since the early days so you'll find out of date documentation and code samples on the Internet. However, the [official documentation](https://developer.android.com/jetpack/compose) will get you pretty far as a getting started guide and will be up to date.

**Missing certain system UI components**:
At the time of writing, Compose is currently lacking a lot of "system" components that I've taken for granted. There is no `SwipeRefreshLayout`.[^swipe-refresh-layout] There is no implementation of Material Preferences. All of the foundational components exist for you to build these yourself but I'm not ready for this kind of committment just yet.


## :anguished: The Ugly

**Parameter lists are inscrutable**:
This picture says it all. ![Jetpack Compose parameter lists](/images/beginning-with-jetpack-compose-beta/params.png)
As a newcomer to these APIs, this can be pretty overwhelming. I've been reading the source code of each function to understand the usage of certain paramaters. I hope the Android Studio team will add some nicer displays of composable function parameter lists.

**Passing callbacks all the way down**:
The Compose documentation recommends splitting your UI into many reusable functions. While this is great for abstraction and reuse, this usually means you need to pass click callbacks through many layers. I've found this can get tedius, especially when you need to refactor code to support click handling. In other declarative UI frameworks this is known as [Prop Drilling](https://kentcdodds.com/blog/prop-drilling). I will probably explore a more global click handling approach using Compose's [CompositionLocal](https://developer.android.com/reference/kotlin/androidx/compose/runtime/CompositionLocal).

**Organization of Compose UI:**
Right now my Compose project consists of a few Kotlin files that each contain many many composable UI elements. These files quickly get complicated and hard to navigate. I've yet to see any guidance about how people should organize their UI definitions in Compose.

[^recyclerview]: This code would easily be 100+ lines using Android's [RecyclerView](https://developer.android.com/guide/topics/ui/layout/recyclerview).
[^ide-tooling]: It hasn't been entirely smooth sailing with the IDE preview. Whenever you refresh the preview it resets its scroll position which makes it really annoying when you are working on one individual component. Additionally, if you write Compose code that crashes at runtime, the preview just shows nothing. I would have appreciated an error message!
[^swipe-refresh-layout]: See this [sample code](https://github.com/android/compose-samples/blob/b8a6e72225b33923d525bc30b754fc0695120316/JetNews/app/src/main/java/com/example/jetnews/ui/SwipeToRefresh.kt#L45) as an example implementation.
