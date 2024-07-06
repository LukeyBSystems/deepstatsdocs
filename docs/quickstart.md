---
layout: default
title: Quickstart Guide
nav_order: 1
---

# Quickstart
This quickstart guide will get you set up with all the necessary things to get started with DeepStats.

### Step 1: Import the package
Window -> Package Manager -> Find Deepstats, import. You can exclude the Demo folder if you don't want it. 

If you're going to include the demo folder, it is recommended to import DeepStats into a new project to avoid script errors if you modify the stat configuration.

### Step 2: Create a StatConfiguration
Find the place in your project that you want to store DeepStats data. 

Right click -> Create -> DeepStats -> Stat Configuration.

Add the stat names to the Stat Types list. They must be unique and a valid name for a C# enum (it will make some attempt to clean up whitespace and capitalisation for you on generation).\
Optional: Add any scalers you might expect to use, these are things that may scale a modifier such as "NearbyTrees", "Number of active poisons"\
Optional: Add any conditions you might expect to use, these are things such as "HasBoost", "InWater"

When you're done, click the "Generate C# scripts" button.

### Step 3: Create a StatProperties
In the same folder as your stat configuration, 

Right click -> Create -> DeepStats -> Stat Properties. This is where you will set default values for your stats, and configure any post-processing.

The default value will be the initial stat value for all instances. 
Use postprocessing to modify the final value of a stat after modifiers

Most projects will only need one StatProperties, although it can be useful for debugging to swap this out sometimes, for example if you're testing extreme values of a stat.

### Step 4: Initialise your scene
Open the scene that will be using DeepStats. 

Then in the toolbar at the top of the Unity Editor, Tools -> DeepStats -> Initialise Scene. This will add a DeepStatsManager gameObject.

Open DeepStatsManager, drag your stat properties Scriptable Object into the reference slot.

### Step 5: Add DeepStats to your game
Open the C# script for the thing that needs stats. This could be your player, enemies, a weapon, anything.
Add the following lines to your class attributes
```
public List<EditorDeepModifier> Modifiers;
private DeepStats _stats = new DeepStats();
```

If your source of stats is also going to be affected by conditions and scalers, add this too:
```
private DeepConditions _conditions = new DeepConditions();
```

Add an Awake() method if your class doesn't have one already, and add
```
foreach (var m in Modifiers)
{
	_stats.AddModifier(m.Value);
}
```

Lastly, DeepStats uses unmanaged objects, so always make sure to dispose them when you are done with them.

```
private void OnDestroy()
{
	_stats.Dispose();
	_conditions.Dispose();
}
```

When you're done, remember to save your class.

### Step 5a. (Optional) Set some conditions and scalers
If you added DeepConditions, you can control these by calling something like
```
_conditions.ModifierScalers[ModifierScaler.NearbyTrees] = totalNearbyTrees;
```
where nearby trees would be calculated by a function you've implemented.

or 

```
_conditions.ModifierConditions[ModifierCondition.InWater] = true;
```
where the boolean would be set depending on whether your character is in water.

### Step 6: Use DeepStats
Add some modifiers to the Modifiers array in the editor. When you need to calculate and use a stat value, call:
```
_stats.UpdateProcessedValues(null, null);
or
_stats.UpdateProcessedValues(_conditions, null);
```
depending on whether you are also using DeepConditions.

Then you can read out your stat values with:
```
var damage = _stats.GetProcessedValue(StatType.Damage);
```