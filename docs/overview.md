---
layout: default
title: Overview
nav_order: 2
---

# Overview

## Quick Overview

### What is a Stat?
A stat is some numerical value in your game which you'll use to drive other behavior, eg.
- A Speed stat can used in your CharacterController to set how fast your character moves
- A Health stat can used in your UnitController to set your characters maximum health

Stat types can also be a sub-type of another stat type - they will inherit all of the modifiers which also apply to their parent. For example, Elemental Damage and Physical Damage can be a sub-type of a generic Damage Stat Type. Fire, Ice and Lightning Damage can be sub-types of Elemental Damage. When calculating Fire Damage, it will also receive any modifiers to Damage and Elemental Damage.

{: .note }
In order to support a common RPG feature of random stat ranges (deals 5-10 damage etc.) without having to create modifiers for each min and max value, DeepStats uses min and max values for all Stats. Modifiers have a property which allows you to modify the min and max value separately, so if you dont want a stat to have a range you just simply leave this property on it's default setting of 'same'.

### What is a Modifier?
Stats can be affected by Modifiers which change the final value of the stat. Some modifiers may alter the base value of a stat, others will multiply the base value by some amount. Some modifiers can interact with other stats such as a conversion from one stat into another, eg.
- +10 Damage
- +20% Health
- 2x Armour

### What is a Tag?
Tags are a set of conditions which modifiers can check for when calculating stats. Each instance of DeepStats has it's own set of tags and Modifiers can require a subset of them to apply, eg.
- Increased Damage With Swords
- Minions Have More Health
- Spells have extra Critical Chance against Undead

### What is a Scaler?
A Scaler is a decimal value that changes how much a Modifier will modify a stat, allowing you to feed aspects of your gameplay into the DeepStats system to create interesting Modifiers eg.
- Increased Damage for each nearby enemy
- Move faster while in water
- Take less damage while inside a shield bubble  
Scalers can be clamped to limit the range of modification. This allows you to create boolean scalers (clamp between 0 and 1) or just to place a limit if a Modifier is too powerful.
