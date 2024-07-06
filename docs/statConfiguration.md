---
layout: default
title: Stat Configuration
nav_order: 2
parent: User Guide
---

# StatConfiguration

The StatConfiguration asset is where you will configure the constants of your stat system.

![example configuration](../images/statConfiguration.jpg)

You can create an instance of this scriptable object in your project with:\
Right Click -> Create -> DeepStats -> StatConfiguration

It is recommended to only have one of these assets in your project, as it will be used to generate the necessary code which the rest of DeepStats will depend on.

A StatConfiguration has the following properties:

### Stat Types
These are the Stat Types you'll be using in your project. If it's a numeric value you want to modify in your game, DeepStats is probably a good place for it.\
Some examples:
- Classic RPG stats: Maximum Health, Damage, Speed, Armour, Agility, Strength etc.
- in a platformer you could add a NumberOfJumps stat so the player can unlock double-jump or triple-jump
- in a racing game you could add a Speed and Steering stat so that the player can customise their vehicle

### Modifier Scalers
These are aspects of your gameplay that can be used to dynamically scale a Modifier value.
Some examples:
- in a racing game, you may have a vehicleDamage scaler which will slow you down and reduce your steering
- in a survival game, you may have a hunger score which makes you do less melee damage

### Modifier Conditions
These are aspects of your gameplay that can be used to toggle a modifier on or off. Note that DeepStats will automatically add a 'None' condition for you, this condition is mandatory for the operation of DeepStats.
Some examples:
- in an ARPG, you may have a modifier where you do more damage to the target enemy if they are currently burning
- in an RTS, you may have a modifier where your units take less damage if they are inside a shield bubble

{: .note }
The names for these elements can be whatever you want, except they must be compatible as a C# enum. This means elements must start with a letter or underscore. DeepStats will also remove any whitespace and convert it to CamelCase.

Once you have finished creating these, hit the 'Generate C# scripts' button. A build will be triggered, and your enums should now be available for use in the editor and in code. Feel free to modify this whenever you like, enums in DeepStats use Editor friendly property drawers so you can re-order and re-name them with the following caveat:

{: .warning }
If you both re-order and re-name an element before clicking Generate, references will be lost. There is no way to identify the original enum if the name has changed and the position has moved. You can avoid this issue by hitting Generate after each operation.

Remember to hit the Generate button when you're done.