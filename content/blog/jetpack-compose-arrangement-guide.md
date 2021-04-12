+++
title = "Jetpack Compose Arrangement: A Visual Guide "
date = "2021-04-12"
description = "A visual guide on how to use Arrangement in Jetpack Compose"
tags = ["android","jetpack-compose"]
+++

One of my favorite blog posts is [Amanda Hill](https://twitter.com/mandybess)'s [Android ImageView ScaleType: A Visual Guide](https://thoughtbot.com/blog/android-imageview-scaletype-a-visual-guide). For some reason, I can never remember Android's different image scaling modes and a visual reference guide really works for me.

This post takes inspiration from Amanda and does the same thing but for Jetpack Compose's [Arrangement](https://developer.android.com/reference/kotlin/androidx/compose/foundation/layout/Arrangement) property.[^notes]

# :left_right_arrow: Row
[`SpaceEvenly`](https://developer.android.com/reference/kotlin/androidx/compose/foundation/layout/Arrangement#spaceevenly)
![1](/images/jetpack-compose-arrangement-guide/row_space_evenly.png)
[`SpaceBetween`](https://developer.android.com/reference/kotlin/androidx/compose/foundation/layout/Arrangement#spacebetween)![1](/images/jetpack-compose-arrangement-guide/row_space_between.png)
[`SpaceAround`](https://developer.android.com/reference/kotlin/androidx/compose/foundation/layout/Arrangement#spacearound)
![1](/images/jetpack-compose-arrangement-guide/row_space_around.png)

# :arrow_up_down: Column
| [`SpaceEvenly`](https://developer.android.com/reference/kotlin/androidx/compose/foundation/layout/Arrangement#spaceevenly) | [`SpaceBetween`](https://developer.android.com/reference/kotlin/androidx/compose/foundation/layout/Arrangement#spacebetween) | [`SpaceAround`](https://developer.android.com/reference/kotlin/androidx/compose/foundation/layout/Arrangement#spacearound) |
|--|--|--|
| ![1](/images/jetpack-compose-arrangement-guide/column_space_evenly.png) | ![1](/images/jetpack-compose-arrangement-guide/column_space_between.png) | ![1](/images/jetpack-compose-arrangement-guide/column_space_around.png) |

# Descriptions

## [`SpaceEvenly`](https://developer.android.com/reference/kotlin/androidx/compose/foundation/layout/Arrangement#spaceevenly)
>  Place children such that they are spaced evenly across the main axis, including free space before the first child and after the last child. Visually: #1#2#3# for LTR and #3#2#1# for RTL.

## [`SpaceBetween`](https://developer.android.com/reference/kotlin/androidx/compose/foundation/layout/Arrangement#spacebetween)
> Place children such that they are spaced evenly across the main axis, without free space before the first child or after the last child. Visually: 1##2##3 for LTR or 3##2##1 for RTL.

## [`SpaceAround`](https://developer.android.com/reference/kotlin/androidx/compose/foundation/layout/Arrangement#spacearound)
> Place children such that they are spaced evenly across the main axis, including free space before the first child and after the last child, but half the amount of space existing otherwise between two consecutive children. Visually: #1##2##3# for LTR and #3##2##1# for RTL

[^notes]: For now, this post excludes the arrangements `Top`/`Bottom`, `Start`/`End`, and `Center` because I deem those are relatively straight forward to internally visualize. :grinning: