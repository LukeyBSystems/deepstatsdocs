---
layout: default
title: Introduction
nav_order: 1
permalink: /
---

# Deep Stats

Deep Stats is a high performance, highly flexible stat and modifier authoring system for Unity. This library is the result of multiple iterations of a stat sytem built for a deep RPG and is designed with 3 main pillars in mind:

### 1. Performance first
The faster the library, the more complex and interesting stats and modifiers we can add to our games. DeepStats uses smart data layouts, caching where possible, and Unity's Burst compiler to take advantage of the speed of LLVM to maximise performance. DeepStats also does not create any garbage after initialisation.

### 2. Maximum flexibility
Interesting modifiers are the backbone of any good stat system. DeepStats includes a tag system so that modifiers can be conditionally applied (Increased Health for Minions, Increased Damage when a Spear is equipped) and a scaling system for dynamic modify values (+5 damage for each nearby enemy). 

DeepStats also supports modifying stats in a variety of interesting ways:
- Add or subtract flat values, multiply stats additively, multiply stats multiplicatively
- Convert one stat into another (eg. Armour converted into Damage)
- Add one stat value as another (eg. Armour added as Damage)
- Apply modifiers from one stat type to another (eg. Increases to Armour also apply to Damage)
- Apply tagged modifiers to a different tag (eg. Damage Modifiers to your minions also apply to you)

DeepStats are also easily composable with a chaining system. Add DeepStats to a weapon, then use the final weapon stats as base values for your character to scale even further. Alternatively, a collection of modifiers can be applied to many instances of DeepStats, allowing you to apply your Player passive Modifiers to your Minions, or have a set of zone Modifiers which affect every enemy in an area.

Finally, customize the post-processing of stats with the math expression parser built into the editor. Use a polynomial function to convert armour rating into a damage reduction percentage, or clamp the min and max values of a stat and round the final value.

For a detailed look at the kinds of modifiers you can create see either the [modifiers overview](/Modifiers) or check out some of the [recipes](/Recipes).

### 3. Designer and programmer friendly
DeepStats treats both designers and programmers equally. Custom editors are built out for configuring your stats, with code generation built into the editors. Designers can add new stat types, conditions, and scalars, then programmers can reference them directly via enums. All the flexibility of Unity Editor authoring, with the performance and programming convenience of enums.

## Getting started
There are a few core concepts that should be understood to get the most out of this library, head over to [getting started](/docs/gettingStarted.md) where you'll find a Quick-Start guide if you just want to get going.
