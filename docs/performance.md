---
layout: default
title: Performance Notes
nav_order: 6
---

# Performance Notes

## General Performance Notes
DeepStats has been written with performance in mind from the start. Generally you shouldn't have to worry about DeepStats affecting your framerate until you start getting into obscene amounts of complex DeepModifiers. On an AMD Ryzen 7 5800X (mid range CPU) running the stress test which has 1000 DeepStatsInstances each recalcuating 1600 assorted DeepModifiers every frame, I get over 300 FPS (0.3ms calculation time).

## Modifier Relative Computational Cost
In order of least to most expensive DeepModifier types per call of `UpdateFinalValues()`
1. Add, SumMultiply, ProductMultiply Modifiers with no Tags or Scalers - can be entirely cached so one upfront cost then "free" onwards
2. Add, SumMultiply, ProductMultiply Modifiers with only self Tags - can be entirely cached but are slightly more expensive to calculate, and must re-calculate when tags change
3. Add, SumMultiply, ProductMultiply Modifiers which depend on self Scalers, target Tags or target Scalers - These are cheap but recalculated each time
4. ModifiersAlsoApplyToStat - Cheap but recalculated each time and depending on source and target types can be equivalent to random access of the Modifier totals which can be slower
5. AddedAs - Requires looping over dependent and target stats to accumulate modifiers. Long chains of AddedAs / ConvertedTo require multiple accumulations
6. ConvertedTo - Same as AddedAs with an additional step to pre-calculate the sum of all conversions so that we don't exceed 100% total

ConvertSelfTags / ConvertTargetTags - These Modifiers can have quite a variable cost. When added, they will search through all modifiers and create copies with the new tags. Depending on the type and number of modifiers copied, they may have a minimal or large performance cost. These you'll need to benchmark yourself.

## Prefer changing Scalers over adding / removing Modifiers
Adding and removing Modifiers can be an expensive operation, especially if DeepStats needs to allocate more memory to fit the new Modifiers in. If you have a performance bottleneck caused by constantly adding and removing modifiers, consider if the same effect could be mimicked by a Modifier with a Scaler that you can toggle between 0 and 1 instead.

## Prefer Scalers for regularly changing Modifiers and Tags for static ones
Modifiers with Scalers are recalculated each time. Modifiers with self Tags are cached if possible. If you are creating a Modifier which you want to bind to a dynamic part of your gameplay you should favour a Scaler for this. If you have a Modifier which will be toggled infrequently, a Tag is better for this.