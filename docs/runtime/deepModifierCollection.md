---
layout: default
title: DeepModifierCollection
nav_order: 2
parent: Runtime Classes
---

# DeepModifierCollection

A DeepModifierCollection is a collection for storing logical groups of Modifiers. It doesn't do anything on it's own, rather it can provide it's Modifiers to other DeepStats instances. You are free to add and remove Modifiers from the collection at any time, and it will update the Modifiers on it's DeepStats children appropriately.

You may come across a situation where you want many different DeepStats instances to have the same subset of stats. This is a perfect time to use a DeepModifierCollection.
- A set of zone Modifiers affecting every enemy in an area
- A set of passive Modifiers that not only affect your player, but also any skills they use and any of their minions
- Faction Modifiers that give every unit in your army a movement speed bonus

It may also be more convenient to use DeepModifierCollections to group Modifiers even if they aren't shared, simply for the convenience of having logical groups you can inspect and display elsewhere.  
For example, your player character may have:
- Traits, a collection of Modifiers chosen at the start of a game
- A passive Modifier tree, which they will allocate points to as they progress
- A set of buffs and debuffs which can be triggered during gameplay
If you want to tell your players where their Modifiers are coming from, grouping them separately will make this much easier.

## Scripting API

### Properties

| Property | Description |
|-|-|
| Modifiers | A readonly List of all Modifiers in this collection |

### Methods

`AddModifier(EditorDeepModifier mod)`  
Add a Modifier to this instance.  

`RemoveModifier(EditorDeepModifier mod)`  
Remove a Modifier from this instance. The Modifier will be removed by looking up a matching ModifierIdentifier on the Modifier.  

`ClearAllModifiers()`  
Remove all owned Modifiers from this instance. Any Modifiers that come from other ModifierCollections will be unaffected.

`AddStatsChild(DeepStats child)`  
Add a DeepStats instance as a child of this collection. Any Modifiers in this collection will now also be part of the DeepStats instances.  

`RemoveStatsChild(DeepStats child)`  
Removes a previously added instance from the list of Children, removing any Modifiers it was providing at the same time.  