
---
layout: default
title: Stat Configuration
nav_order: 2
parent: User Guide
---

# StatConfiguration

The StatConfiguration asset is where you will configure the constants of your stat system.

![example configuration](../images/dependentRule.jpg)

You can create an instance of this scriptable object in your project with:\
Right Click -> Create -> DeepStats -> StatConfiguration\
It is recommended to only have one of these assets in your project, as it will be used to generate the necessary code which the rest of DeepStats will depend on.

A StatConfiguration has the following properties

## Stat Types
These are the Stat Types you'll be using in your project. If it's a numeric value you want to modify in your game, DeepStats is probably a good place for it.\
Some examples:
- Classic RPG stats: Maximum Health, Damage, Speed, Armour, Agility, Strength etc.
- If you're making a platformer and want the player to unlock double-jump, you could add a NumberOfJumps stat.
- If you're making a racing game and want to have speed boosts and oil slicks, you could add a Speed and Steering stat.

## Modifier Scalers
These are aspects of your gameplay that can be used to dynamically change a Modifier
Some examples:
- 
