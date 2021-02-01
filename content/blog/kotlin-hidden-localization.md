+++
title = "Beware Kotlin's Hidden Localization"
date = "2021-01-31"
description = "A tale of string localization and formatting in Kotlin"
tags = ["kotlin"]
+++

Recently, I had a fun bug at work which ultimately stemmed from a very simple problem — hidden localization. I needed to interpolate a String in Kotlin but didn't want to use Kotlin's string literal interpolation feature.[^1] Therefore I opted for Java's `String.format` method; Kotlin provides a handy `fun String.format(vararg args: Any?): String` extension for this.

```kotlin
val string = "%d dollars".format(2)
println(string) // Prints "2 dollars" as expected
```

However, I had missed an important part of [the documentation](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.text/format.html#format):
>  Uses this string as a format string and returns a string obtained by substituting the specified arguments, using the **default locale**.

```kotlin
Locale.setDefault(Locale("ar")) // Set locale to Arabic
val string = "%d dollars".format(2)
println(string) // Prints "٢ dollars"
```

I had forgotten that some languages have non-latin numerals! This caused a bug in some other code that expected latin numerals. The fix is trivial to tell Kotlin to not use any localization:

```kotlin
Locale.setDefault(Locale("ar")) // Set locale to arabic
val string = "%d dollars".format(2, null) // Format without localization
println(string) // Prints "2 dollars" as expected
```

Next time you reach for Kotlin's `String.format`, make sure you double check whether you need localization or not!

[^1]: In hindsight, I'm not sure why I didn't just use string literal interpolation.