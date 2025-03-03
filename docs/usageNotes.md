---
layout: default
title: Usage Notes
nav_order: 6
---

# Usage Notes

## Delete demo folder when no longer needed
The demo folder contains a number of Stat Types, Tags and Scalers which will get picked up by DeepStats. To prevent getting extra types you don't want, delete the entire demo folder once you're done with it.

## Using generated enums
A feature of DeepStats is code generation, so the various types can be accessed directly in code using enums instead of relying on referencing scriptable objects in the inspector. The scriptable object reference based approach can be slow and clunky - it's easy to forget to assign a reference, usages aren't easily searchable, and it requires extra boilerplate code. Using the generated enums can be a lot faster to work with and is my preference, but be aware that they aren't resilient to renaming like the scriptable object workflow is. You'll have to manually fix names in your code if you change your stat configuration. It's up to you to decide which workflow suits you better.

## Don't move or rename files in the DeepStats packages folder
DeepStats relies on files being in specific locations. If you move or rename any of the DeepStats files, you will likely break DeepStats, so don't touch them unless you're prepared to fix things yourself.

## EditorDeepModifiers create a DeepModifier value type so they should be treated as immutable.
Once an EditorDeepModifier has been accessed (by reading the `.Value` property), it cannot be changed because it builds a struct internally which is what DeepStatsInstances actually use. This generally means that any changes made to an EditorDeepModifier in the inspector during gameplay will not be reflected in the Modifier.

## Remove and Add Modifiers if you must change them
If you must update a Modifier, you can ensure the updated values are applied by removing the Modifier from each DeepStatsInstance (Instances will find the Modifier by ID lookup so the Modifier does not have to match), then add it back again.

## Always prefer to create Modifiers using the EditorDeepModifier class
You can create a DeepModifier struct and this will work fine for simple Modifiers, however the EditorDeepModifier class provides a number of safety checks to ensure your Modifiers are created correctly so should always be preferred. Only consider using the struct version if you're getting a lot of memory pressure from creating lots of Modifier objects and you know what you're doing.