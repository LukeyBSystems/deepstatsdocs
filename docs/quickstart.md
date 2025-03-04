---
layout: default
title: Quick Start Guide
nav_order: 3
---

## Quickstart

### Step 1: Import the package
Window -> Package Manager -> Find Deepstats, import. You can exclude the Demo folder if you don't want it. 

Uncheck the Demo folder import if you don't want it. If you're going to include the demo folder, it is recommended to import DeepStats into a new project to avoid script errors if you modify the stat configuration.

### Step 2: Configure your types
Create Stat Types ScriptableObjects wherever you like in your Assets folder. Right click -> Create -> DeepStats - Stat Type. These are the stats of your stat system.  
The names must be unique and a valid name for a C# enum (DeepStats will make some attempt to clean up whitespace and capitalisation for you on generation).  

Optional: Add any Scalers you might expect to use, these are things that may scale a modifier such as "NearbyTrees", "Number of active poisons"\
Optional: Add any Tags you might expect to use, these are things such as "Undead", "Ranged"

### Step 3: Create a StatConfiguration
Find the place in your project that you want to store DeepStats data. Right click -> Create -> DeepStats -> Stat Configuration.

When you're done, click the "Generate C# scripts" button.

### Step 4: Add a DeepStatsManager to your scene
Open the scene that will be using DeepStats. 

Then in the toolbar at the top of the Unity Editor, Tools -> DeepStats -> Initialise Scene. This will add a DeepStatsManager gameObject and create a starter StatConfiguration object for you in the Assets directory if your project doesn't already have one.

Open DeepStatsManager and set your StatConfiguration Scriptable Object in the reference slot.

### Step 5: Create a script with DeepStats on it

This could be your player, enemies, a weapon, anything. 

{: .note }
The DeepStatsInstance class uses unmanaged memory, so always remember to call Dispose() on them when you're done.

```cs
using System.Collections.Generic;
using LukeyB.DeepStats.User;
using UnityEngine;

[System.Serializable]
public class UnitScaler
{
    public ModifierScalerSO Scaler;
    public float ScalerValue;
}

public class GameUnit : MonoBehaviour
{
    public List<EditorDeepModifier> Modifiers;
    public List<ModifierTagSO> UnitTags;
    public List<UnitScaler> UnitScalers;

    private DeepStatsInstance _stats;

    public void Awake()
    {
        _stats = new DeepStatsInstance();

        foreach (var tag in UnitTags)
        {
            _stats.SetTag(tag, true);
        }

        foreach (var scaler in UnitScalers)
        {
            _stats.SetScaler(scaler.Scaler, scaler.ScalerValue);
        }

        foreach (var m in Modifiers)
        {
            _stats.AddModifier(m.Value);
        }

        _stats.UpdateFinalValues(null);

        for (var i = 0; i < DeepStatsConstants.NumStatTypes; i++)
        {
            var statType = (StatType)i;
            var statValue = _stats[statType];
            Debug.Log($"{statType}: {statValue}");
        }
    }

    private void OnDestroy()
    {
        _stats.Dispose();
    }
}

```

### Step 7: Use DeepStats
Add some modifiers to the Modifiers array in the editor. When you run your game, you'll see the calculated stat values in the console logs.
