---
layout: default
title: Introduction
nav_order: 1
permalink: /
---

# Deep Stats

Deep Stats is a high performance, flexible stat management and authoring library for Unity. This library is the result of multiple iterations of a stat sytem built for a deep RPG and is designed with 3 main pillars in mind:

### 1. Performance first
The faster the library, the more complex and interesting stats and modifiers we can add to our games. DeepStats uses smart data layouts, caching, and Unity's Burst compiler to take advantage of the speed of LLVM to maximise performance. Easily process millions of stats and modifiers per second with minimal impact on frametime.

### 2. Maximum flexibility
Interesting modifiers are the backbone of any good stat system. DeepStats supports scaling stats in a variety of ways as well as conversions between stat types or adding one stat value as another. DeepStats also supports conditional modifiers ("While Burning", "If Hit Recently" etc.) and scaling modifiers by a gameplay element ("+5 damage for each nearby enemy" etc.). For a detailed look at the kinds of modifiers you can create see either the [modifiers overview](/Modifiers) or check out some of the [recipes](/Recipes).
DeepStats are also composable; put stats and modifiers on a weapon, then use the final weapon stats as base values for your character to scale even further. Alternatively, group stat modifiers together and merge them to easily add more sources later such as new passive trees or area specific modifiers you can apply to all units in a zone.
Finally, customize the post-processing of stats. Convert armour rating into a damage reduction % using a polynomial function. Round your stat values to keep them clean throughout your game. Clamp the maximum value of one stat to another stat, so you can create modifiers like (+10% maximum resistance).

### 3. Designer and programmer friendly
DeepStats treats both designers and programmers equally. Custom editors are built out for configuring your stat systems, with code generation built into the editors. Designers can add new stat types, conditions, and scalars, then programmers can reference them directly via enums. An Editor Enum class is included which supports re-ordering and renaming enums so that references aren't lost when the enums are modified. All the flexibility of Unity Editor authoring, with the performance and programming convenience of enums.

## Getting started
There are a few core concepts that should be understood to get the most out of this library, head over to [getting started](/docs/gettingStarted.md) where you'll find a Quick-Start guide if you just want to get going.

