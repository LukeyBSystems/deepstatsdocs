---
layout: default
title: Stat Configuration
nav_order: 1
parent: Configuration Components
---

# Stat Configuration

The StatConfiguration asset is where you will configure the constants of your stat system.

![example configuration](../../images/statConfiguration.jpg)

You can create an instance of this scriptable object in your project with:\
Right Click -> Create -> DeepStats -> StatConfiguration

It is recommended to only have one of these assets in your project, as it will be used to generate the necessary code which the rest of DeepStats will depend on.

## Configuring DeepStats Types
Stat Types, Scalers and Tags are all Scriptable Objects. You can create them in whatever folder you like within your project. Create a new object by Right Click -> Create -> DeepStats -> Configurations and select the type you want to create.

{: .note }
The names for these Scriptable Objects must be compatible as a C# enum. This means names must start with a letter or underscore, it also means no duplicate names. DeepStats will also remove any whitespace and convert it to CamelCase. If a name is not compatible, DeepStats will attempt to rename your ScriptableObjects for you to make them valid. To keep things predictable, it is recommended to name your stats following C# enum conventions.

Once you have finished creating these, hit the 'Generate C# scripts' button. A build will be triggered, and your Stats will be available for use in the editor and in code as enums. You can modify the StatConfiguration and regenerate whenever you like, although keep in mind if you have referenced one of the types by its enum instead of its ScriptableObject and you rename the ScriptableObject, you'll need to go back and update the enum reference.

{: .warning }
Don't ever modify the generated enums directly, always modify them by updating your ScriptableObjects then regenerating code. This will ensure everything is in sync.

### Stat Types
These are the Stat Types you'll be using in your project. If it's a numeric value you want to modify in your game, DeepStats is probably a good place for it.\
Some examples:
- Classic RPG stats: Maximum Health, Damage, Speed, Armour, Agility, Strength etc.
- In a platformer you could add a NumberOfJumps stat so the player can unlock double-jump or triple-jump
- In a racing game you could add a Speed and Steering stat so that the player can customise their vehicle

{: .note }
Stats are calculated in the order of your StatConfiguration. This is important for dependent Modifiers such as ConvertedTo (Fire converted to Ice) / AddedAs (Fire added as Ice) to prevent circular dependencies. If you want to convert Health to Armour, make sure Health comes first in your StatConfiguration.

![dependent rule](../../images/dependentRule.jpg)

### Modifier Scalers
These are aspects of your gameplay that can be used to dynamically scale a Modifier value.
Some examples:
- In a racing game, you may have a vehicleDamage scaler which you could use to scale a speed Modifier and a handling Modifier
- In a survival game, you may have a hungerScore scaler which you could use to scale a max stamina Modifier and a damage Modifier

### Modifier Tags
These are less dynamic aspects of your game that can be used to create requirements for a Modifier to activate
Some examples:
- In an ARPG, you may have Human, Minion, Melee, Spell, Undead tags. These could be used to create Modifiers that only apply to the Player and not to their Minions, or to create a spell which does more damage against Undead Melee units.
- In an RTS, you may have Melee, Ranged, Armoured, Biological, Shielded tags. These could be used to create a shield upgrade Modifier for your faction that only affects Shielded units, or create a unit that has a Modifier giving it bonus damage against Armoured enemies.