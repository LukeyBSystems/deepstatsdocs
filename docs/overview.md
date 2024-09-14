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

### What is a Modifier?
Stats can be affected by Modifiers which change the final value of the Stat. Some Modifiers may alter the base value of a Stat, others will multiply the base value by some amount. Some modifiers can interact with other Stats such as a conversion from one Stat into another, eg.
- +10 Damage
- +20% Health
- 2x Armour

### What is a Tag?
A Tag is a flag you can set that tells DeepStats which Modifiers to apply when calculating stats. Instances might have many tags, and Modifiers can require a subset of them, eg.
- Increased Damage With Swords
- Minions Have More Health
- Spells have extra Critical Chance against Undead

### What is a Scaler?
A Scaler is a decimal value that changes how much a Modifier will modify a stat, allowing you to feed aspects of your gameplay into the DeepStats system to create interesting Modifiers eg.
- Increased Damage for each nearby enemy
- Move faster while in water
- Take less damage while inside a shield bubble

## Things to know

### All Stats are have a min and max value
In order to support a common RPG feature of random stat ranges (deals 5-10 damage etc.) without having to create modifiers for each min and max value, DeepStats uses stat ranges for all Stats. Throughout DeepStats, 'Raw' values refer the stat range value and 'Final' values refer to the randomised value between the range. Modifiers can set 'same' or 'different' values for the min and max modification. If you don't want a stat to have a range, just leave the 'Set Min / Max Values' property at 'Same' so that the random final value is always the same.

![same min max](../images/minMaxSame.jpg)

![different min max](../images/minMaxDifferent.jpg)

#