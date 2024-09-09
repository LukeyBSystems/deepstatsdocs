---
layout: default
title: DeepStatsManager
nav_order: 3
parent: Configuration Components
---

# Deep Stats Manager

The DeepStatsManager GameObject is required in any scene of your game that uses DeepStats. It builds the static data structures and objects needed to perform calculations.

The easiest way to add the Manager to the scene is via the toolbar at the top of the Unity Editor, \
Tools -> DeepStats -> Initialise Scene.

After you've added the DeepStatsManager, locate it in the scene object list and assign your Configuration and Properties ScriptableObjects.

{: .note }
DeepStatsManager initialises a number of required properties at startup and will require a restart if you need to update the Configuration or Properties.