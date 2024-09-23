---
layout: default
title: Demo Scenes
nav_order: 10
---

In the Demo/Scenes folder of DeepStats you will find two folders:
1. Samples can be used as a guide for how to build with DeepStats.
2. Tests contains a Stress Test you can use on your own platform to ensure you're getting the performance you want.

The Demos require all of the ScriptableObjects defined in the DeepStats Configuration folder, as well as the latest code generated from the demo DeepStatsConfiguration object. If you make any changes to the Demo Stat Configuration, most likely the demos will stop working. It's worth having a quick browse of this folder to familiarise yourself with what has been configured if you want to understand the demos further.

## Samples
### Sample 1: Modifier Sandbox
Use this scene to familiarise yourself with DeepStats. Add and remove Modifiers and the stats printed will update in realtime.

### Sample 2: Environmental Effects
This scene demonstrates the use of Scalers to update the Stats of the Player. The player has 3 Modifiers, and Scalers control their affects when the Player is in water or near trees.

### Sample 3: Equipment Swapping
This scene demonstrates the use of Tags to conditionally apply Modifiers. You can swap between Unarmed, Sword, or Spear type weapons. You can also randomise the Player modifiers by pressing 'R'. Note how some Modifiers specify that they only apply to Spears or Swords and observe the Stats after swapping weapons. There are also some AddedAs / ConvertedTo Modifiers added to demonstrate what happens when you convert Physical to Elemental Damage.

This scene also utilises the Added Stat Source functionality of DeepStats. Note how the weapons have their own Modifiers and Stats. The final stats of the weapon then become the base stats of the player.

### Sample 4: Summoner and Minions
This scene demonstrates using a DeepModifierCollection to create a passive skill tree style system where the Players Modifiers can also apply to their Minions. Tags are used to conditionally apply Modifiers depending on the type of DeepStats instance. It also demonstrates the use of a Tag Conversion modifier to grant benefits to the Player from their Minion Modifiers.
