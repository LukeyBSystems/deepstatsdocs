---
layout: default
title: DeepStats
nav_order: 4
parent: Core Components
---

# The DeepStats Class
The DeepStats class is how you'll access and modify Stats throughout your game. It contains all of the methods for collecting modifiers and calculating stats.

## Adding and Removing Modifiers
There are two ways to add Modifiers to a DeepStats instance.

#### Add Modifiers Directly
Add Modifiers directly to a DeepStats instance via the `DeepStats.AddModifier(myModifier)` method. This can be used in simple cases where all you need is a few Modifiers and a basic Stats setup, but otherwise it's more likely that option 2 will be more useful and convenient.

### Add Modifiers via a DeepModifierCollection
Create a DeepModifierCollection which can store many Modifiers, then add the whole collection at once to a DeepStats instance using `DeepModifierCollection.AddStatsChild(deepStatsInstance)`. Any Modifiers added or removed from the DeepModifierCollection will cascade into all of the DeepStats children. This allows you to share a single collection of Modifiers with many DeepStats instances.

For example, this can be used for:
- Giving your Players a Passive Skill Tree, then applying the same passives to all spells and minions that the Player uses.
- Create a set of Zone Modifiers which apply to all monsters in an area.
- Easily add and remove sets of Modifiers as your player equips new gear.
- Create an upgrade system for your RTS, where a Player can research upgrades that affect their entire army.

## Add a DeepStats instance as a stat source
A DeepStats instance can also be used as a source of stats to another DeepStats instance using the `DeepStats.AddAddedStatsSource(childDeepStats)`. When calculating stat values, all of the sources will be calculated first then added as though they are Add style Modifiers.

You can use this to have multiple layers of stats. For example, a players weapons and armour could have their own Modifiers. The final stats of the equipment will then be scaled again by the players own Modifiers.

## Scripting API

### Properties

| Property | Description |
|-|-|
| CachedCount | Number of Modifiers which were able to be cached after setting self DeepConditions on the DeepStats instance with the SetSelfConditions method |
| FinalValuesAreStale | Boolean indicating if the final values need to be re-calculated by calling `UpdateFinalValues()` |
| Modifiers | Call `foreach (var mod in Modifiers.Owned)` to read out each Modifier added to this instance, or instead `foreach (var mod in Modifiers.All)` property to read out all Modifiers from either this or any ModifierCollections which are supplying Modifiers. AllCount and OwnedCount are also available |

### Methods

`AddModifier(Modifier mod)`  
Add a Modifier to this instance.  

`RemoveModifier(Modifier mod)`  
Remove a Modifier from this instance. The Modifier will be removed by looking up a matching ModifierIdentifier on the Modifier.  

`ClearAllModifiers()`  
Remove all owned Modifiers from this instance. Any Modifiers that come from other ModifierCollections will be unaffected.

`AddAddedStatsSource(DeepStats stats)`  
Add a DeepStats instance as stat source to this instance (see 'Add a DeepStats instance as a stat source' above).

`RemoveAddedStatsSource(DeepStats stats)`  
Remove a DeepStats instance from the stat sources of this instance.

`UpdateFinalValues(DeepStats target)`  
Re-calculate final stat values, which will also update the raw values in the process. If there is no target, null can be passed in instead.

`GetRawValue(StatType type)`  
Returns a float2 which is the raw value of the StatType. A raw value is the stat range before the random sample and any post-processing

`GetFinalValue(StatType type)`  
Returns a float which is the final value of the StatType. A final value is the sampled value from between the raw range, after any post-processing

`GetRawModifierTotal(StatType statType, ModifierType modifyType)`  
Returns a float2 which is the total of a Modifier type to a Stat type. You could use this method to show totals used in calculating a stats final values. Acceptable ModifierType's are
- Add
- SumMultiply
- ProductMultiply
- AddedAs (returns the total added from both AddedAs and ConvertedTo modifier types)
