---
layout: default
title: DeepStatsManager
nav_order: 3
parent: Configuration Components
---

# Deep Stats Manager

The DeepStatsManager GameObject is required in any scene of your game that uses DeepStats. It builds the static data structures and objects needed to perform calculations.

{: .note }
DeepStatsManager is effectively a singleton and is also marked with 'DontDestroyOnLoad' so that the data structures continue to exist across scenes. It will also ensure there is only one instance at any time, so it's fine to have one in each scene for testing and also swap between scenes at runtime without issue.

The easiest way to add the Manager to the scene is via the toolbar at the top of the Unity Editor, \
Tools -> DeepStats -> Initialise Scene.
If you dont already have a StatConfiguration scriptable object in your project, this will also create one for you in the Assets folder

After you've added the DeepStatsManager, locate it in the scene object list and ensure your StatConfiguration is assigned.

{: .note }
DeepStatsManager initialises a number of required properties at startup. You will need to restart your game if you need to update the Configuration.
