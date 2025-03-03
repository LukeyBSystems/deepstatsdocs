---
layout: default
title: DeepStatsInstance
nav_order: 1
parent: Runtime Classes
---

# DeepStatsInstance
The DeepStatsInstance class is how you'll access and modify stats throughout your game. It contains all of the methods for collecting modifiers and calculating stats.

{: .note }
DeepStatsInstance objects contain unmanaged memory. Always call `Dispose()` on them when you're done with them, or in the OnDestroy of the container GameObject.

## Adding and Removing Modifiers
There are two ways to add Modifiers to a DeepStats instance.

### Add Modifiers Directly
Add Modifiers directly to a DeepStats instance via the `instance.AddModifier(myModifier)` method. This can be used in simple cases where all you need is a few Modifiers and a basic stats setup, but otherwise it's more likely that the next option will be more useful and convenient.

{: .note }
Even though there is an overload that accepts an EditorDeepModifier object, Modifiers are always stored by their underlying value type so they can be compatible with Burst. This means that any changes to the object will not be reflected in the instance stats. Remember, if you need to change a Modifier, remove it from the stats instance, make the changes, then add it back.

### Add Modifiers via a DeepModifierCollection
Create a [DeepModifierCollection](runtime/deepModifierCollection.md) which can store many Modifiers, then register your DeepStatsInstance as a child with `DeepModifierCollection.AddStatsChild(deepStatsInstance)`. Any Modifiers added or removed from the DeepModifierCollection will cascade into all of the DeepStatsInstance children. This allows you to share a single collection of Modifiers with many DeepStats instances.

For example, this can be used for:
- Giving your Players a Passive Skill Tree, then applying the same passives to all spells and minions that the Player uses.
- Create a set of Zone Modifiers which apply to all monsters in an area.
- Easily add and remove sets of Modifiers as your player equips new gear.
- Create an upgrade system for your RTS, where a Player can research upgrades that affect their entire army.

## Add a DeepStats instance as a stat source to another Instance
A DeepStats instance can also be used as a source of stats to another DeepStats instance using the `instance.AddAddedStatsSource(childInstance)`. When calculating stat values, all of the source stats will be calculated first then added as though they are Add style Modifiers.

You can use this to have multiple layers of stats. For example in an ARPG, a players weapons and armour could have their own Stats and Modifiers. The final stats of the equipment will then form the base stats of the player, to be scaled again by the players passive Modifiers.

## Configuring Tags and Scalers
Each DeepStatsInstance has its own set of Tags and Scalers. These will be used when calculating Modifiers to determine which Modifiers apply and the value of any scaled Modifiers. Set values of these using the `SetScaler` or `SetTag` methods.

## Scripting API

### Properties

| Property | Description |
|-|-|
| CachedCount | Number of Modifiers which were able to be cached after setting self DeepConditions on the DeepStats instance with the SetSelfConditions method |
| FinalValuesAreStale | Boolean indicating if the final values need to be re-calculated by calling `UpdateFinalValues()`. Any changes to the Modifiers or Tags of this instance will set this to true. |
| Modifiers | Call `foreach (var mod in Modifiers.Owned)` to read out each Modifier added to this instance, or instead `foreach (var mod in Modifiers.All)` property to read out all Modifiers from either this or any ModifierCollections which are supplying Modifiers. AllCount and OwnedCount are also available |

### Methods

`AddModifier(EditorDeepModifier mod)`  
Add a Modifier to this instance.  

`RemoveModifier(EditorDeepModifier mod)`  
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
Returns a float2 which is the raw value of the StatType. A raw value is the stat range before any post-processing.

`GetFinalValue(StatType type)`  
Returns a float2 which is the final value of the StatType. A final value is the value after any post-processing and Final type Modifiers.

`GetRandomFinalValue(StatType type)`
A convenience function which returns a float sampled from between the range of the final value.

`GetRawModifierTotal(StatType statType, ModifierType modifyType)`  
Returns a float2 which is the total of a Modifier type to a Stat type. You could use this method to show totals used in calculating a stats final values. Acceptable ModifierType's are
- Add
- SumMultiply
- ProductMultiply
- AddedAs (returns the total added from both AddedAs and ConvertedTo modifier types)

`SetScaler(ModifierScaler scaler, float value)`
Sets a scaler value on this DeepStatsInstance using an enum Scaler.

`SetScaler(ModifierScalerSO scaler, float value)`
Sets a scaler value on this DeepStatsInstance using a ScriptableObject Scaler.

`SetTag(ModifierTag tag, bool value)`
Sets a Tag true or false on this DeepStatsInstance using an enum Tag.

`SetTag(ModifierTagSO tag, bool value)`
Sets a Tag true or false on this DeepStatsInstance using an ScriptableObject Tag