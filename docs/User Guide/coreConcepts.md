---
layout: default
title: Core Concepts
nav_order: 1
parent: User Guide
---

# DeepStats Core Concepts

1. All Stats are have a min and max value\
In order to easily support a common RPG feature of random stat ranges (deals 5-10 damage etc.) without having to create modifiers for each min and max value, DeepStats uses stat ranges for all Stats.\
Modifiers can set same or different values for the min and max. If you don't want a stat to have a range, you can leave all modifiers at 'same'.

![same min max](../../images/minMaxSame.jpg)
![same min max](../images/minMaxSame.jpg)
![same min max](../../../images/minMaxSame.jpg)

![different min max](../../images/minMaxDifferent.jpg)

2. Stats are calculated in the order of your StatConfiguration\
This is important for dependent Modifiers such as ConvertedTo (Fire converted to Ice) / AddedAs (Fire added as Ice) between stat types to prevent circular dependencies.\
If you want to convert Health to Armour, make sure Health comes first in your StatConfiguration.