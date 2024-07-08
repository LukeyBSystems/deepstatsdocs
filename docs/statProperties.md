---
layout: default
title: Stat Properties
nav_order: 3
parent: User Guide
---

# Stat Properties

The StatProperties Scriptable Object is where you will define the initial values for your Stats and any Post-Processors for them.

![example properties](../images/statProperties.jpg)

You can create an instance of this scriptable object in your project with:\
Right Click -> Create -> DeepStats -> StatProperties

You can have multiple versions of StatProperties, such as a regular version and a debug version for testing some stat behaviors. Swap them out by changing the referenced instance in your scene's DeepStatsManager.

A StatProperties has the following properties:

### Default Value
Set the default base value for the stat. This will be the starting point for all future stat calculations.

### PostProcessing
Use up to 3 final stat values in a post-processing function to modify a stat value.

![example function](../images/postProcessing.jpg)

The expression parser will replace STAT1, STAT2 and STAT3 respectively with the Stat Type selected in the dropdown.

If the expression is left blank, the final Stat value will be un-changed.