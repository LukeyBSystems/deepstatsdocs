---
layout: default
title: Getting Started
nav_order: 2
---

# Getting Started

## Quick Overview

### What is a Stat?
A stat is some numerical value in your game which you'll use to drive other behavior, eg.
- A Speed stat can used in your CharacterController to set how fast your character moves
- A Health stat can used in your UnitController to set your characters maximum health

### What is a Modifier?
Stats can be affected by Modifiers which change the final value of the Stat. Some Modifiers may alter the base value of a Stat, others will multiply the base value by some amount. Some modifiers can interact with other Stats such as a conversion from one Stat into another.

Modifiers can be affected by Modifier Scalers which will alter the modifier value, allowing you to create dynamic modifiers that depend on your gameplay.

Modifiers can also be conditionally applied by checking for Tags on itself or a target.

### What is a Tag?
A Tag is a flag you can set that tells DeepStats which modifiers to apply when calculating stats. Instances might have many tags, depending on how detailed you want your modifiers to be. 
For example:
Your main character might have a 'Player' tag, and when they have a sword equipped they might also gain the 'Melee' and 'Sword' tags. 
The player's 'Raise Zombie' spell would create minions with the 'Minion', 'Melee', 'Unarmed' tags.

### What is a Scaler?
A Scaler is a decimal value that changes how much a Modifier will modify a stat. These are usually aspects of your gameplay that you may use to create interesting Modifiers, such as additional damage for each neaby enemy or reduced movement speed while affected by a Slow status ailment.



## Things to know

### All Stats are have a min and max value
In order to support a common RPG feature of random stat ranges (deals 5-10 damage etc.) without having to create modifiers for each min and max value, DeepStats uses stat ranges for all Stats. Modifiers can set 'same' or 'different' values for the min and max modification. If you don't want a stat to have a range, just leave the 'Set Min / Max Values' property at 'Same' so that the random final value is always the same.

![same min max](../images/minMaxSame.jpg)

![different min max](../images/minMaxDifferent.jpg)

#