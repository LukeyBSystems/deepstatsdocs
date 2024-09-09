---
layout: default
title: Quick Start Guide
nav_order: 5
---

## Quickstart

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

The default value will be the initial base value for all instances. 
Use postprocessors to modify the final value of a stat after modifiers.

Most projects will only need one StatProperties, although it can be useful for debugging to swap this out sometimes, for example if you're testing extreme values of a stat.

### Step 4: Initialise your scene
Open the scene that will be using DeepStats. 

Then in the toolbar at the top of the Unity Editor, Tools -> DeepStats -> Initialise Scene. This will add a DeepStatsManager gameObject.

Open DeepStatsManager, drag your StatProperties Scriptable Object into the reference slot.

### Step 5: Create a script with DeepStats on it

This could be your player, enemies, a weapon, anything.

```cs
    public class DeepStatsClass : MonoBehaviour
    {
        public List<EditorDeepModifier> Modifiers;

        private DeepStats _stats;
        private DeepConditions _conditions;

        public void Awake()
        {
            _stats = new DeepStats();
            _conditions = new DeepConditions();

            foreach (var m in Modifiers)
            {
                _stats.AddModifier(m.Value);
            }

            _stats.UpdateFinalValues(_conditions, null);

            for (var i = 0; i < DeepStatsConstants.NumStatTypes; i++)
            {
                var statType = (StatType)i;
                var value = _stats.GetFinalValue(statType);
                Debug.Log($"{statType}: {value}");
            }
        }

        private void OnDestroy()
        {
            _stats.Dispose();
            _conditions.Dispose();
        }
    }
```

### Step 6: Use DeepStats
Add some modifiers to the Modifiers array in the editor. When you run your game, you'll see the calculated stat values in the console logs.
