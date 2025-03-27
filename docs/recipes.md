---
layout: default
title: Recipes
nav_order: 9
---

# Recipes

This list will try to include answers for common implementations, feel free to email me if you can't find an answer on this list.

### I want to create tiered modifiers like Path of Exile, where equipment can roll different tiers of the same modifier.
Take a look at TieredModifier / TieredRandomizedModifier [here](runtime/otherModifierTypes.md), depending on your needs you may be able to use this class directly or make some small modifications to suit. When you're rolling items, grab a random tier from a random assortment of TieredModifiers.

### I want to be able to upgrade items, increasing the value of the modifiers.
Take a look at TieredModifier / TieredRandomizedModifier [here](runtime/otherModifierTypes.md) . Store the current tiers of each Modifier on an item, and when you want to upgrade it:
1. Remove the old modifier from the DeepStatsInstance (you can grab any tier from the TieredModifier instance and use that to remove, they all have the same ID)
2. Call the "GetTieredModifier()" method on the TieredModifier with the next tier up to get a stronger version of the same modifier
3. Add the stronger modifier back to the item
