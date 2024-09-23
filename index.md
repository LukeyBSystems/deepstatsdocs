---
layout: default
title: Introduction
nav_order: 1
permalink: /
---

# Deep Stats

Deep Stats is a high performance, highly flexible Stat and Modifier authoring system for Unity. 

This library is designed with 3 main pillars in mind:

### 1. Maximum flexibility
Interesting modifiers are the backbone of any good stat system. DeepStats includes a tag system so that modifiers can be conditionally applied (+10 Health for Minions, +5 Damage when a Spear is equipped) and a scaling system for dynamic modify values (+5 damage for each nearby enemy). 

DeepStats also supports a variety of different ways to create interesting modifiers:
- Add or subtract flat values, multiply stats additively, multiply stats multiplicatively (eg. +5 Damage, + 20% Damage, 2 x Damage)
- Convert one stat into another (eg. Armour converted into Damage)
- Add one stat value as another (eg. Armour added as Damage)
- Apply modifiers to one stat type to another (eg. Increases to Armour also apply to Damage)
- Apply tagged modifiers to a different tag (eg. Damage Modifiers for your Minions also apply to you)

DeepStats are also easily composable with a chaining system. Add DeepStats to a weapon, then use the final weapon stats as base values for your character to scale even further. Alternatively, a collection of modifiers can be applied to many instances of DeepStats, allowing you to apply your Player passive Modifiers to your Minions, or have a set of zone Modifiers which affect every enemy in an area.

Finally, customize the post-processing of stats with the math expression parser built into the editor. Use a polynomial function to convert armour rating into a damage reduction percentage, or clamp your Resistance stat between 0 and 100 then round the final value. Additional Modifier types are available to modify the final value of a stat.

For a detailed look at the kinds of modifiers you can create see either the [modifiers overview](/Modifiers).

### 2. Simple and Fast
The faster the library, the more complex and interesting stats and modifiers we can add to our games. DeepStats uses smart data layouts, carefully applied unsafe code, caching where possible, and Unity's Burst compiler to take advantage of the speed of LLVM to maximise performance. DeepStats also does not create any garbage after initialisation. In the stress test with 1000 DeepStats instances each with 1600 assorted modifiers (1.6M total modifiers), it takes around 0.3ms to update all of them on a mid-range CPU. It does not require any multi-threading, background tasks, async-await style programming to reach these speeds, so DeepStats is incredibly simple to use.

### 3. Designer and programmer friendly
DeepStats treats both designers and programmers equally. Custom editors are built out for configuring your stats, with code generation built into the editors. Designers can add new stat types, tags and scalars, then programmers can reference stat types, tags and scalers directly via enums. All the flexibility of Unity Editor authoring, with the performance and programming convenience of enums.

## Getting started
There are a few core concepts that should be understood to get the most out of this library, head over to [Overview](/docs/overview.md) to... get started.

Alternatively if you just want to figure it out on your own, the bare minimum setup guide can be found in the [Quick Start](/docs/quickstart.md) guide.
