---
layout: default
title: EditorDeepModifier
nav_order: 2
parent: Runtime Classes
---

# EditorDeepModifier

This is the authoring class for creating Modifiers via the Unity Editor. Use it's custom editor to create a wide range of Modifiers. Modifiers can be added to DeepStats and DeepModifierCollections

## Types of Modifier

#### Add
 Adds a flat value to the target stat.  
 eg. `TargetStat + 5`

### SumMultiply
Adds a value with all the other SumMultiply mods, before multiplying the target stat.  
eg. `TargetStat * (1 + mod1 + mod2 + mod3 + ...)` 

### ProductMultiply
Multiplies the target stat by a value.  
eg. `TargetStat * 2`

### AddedAs
Multiplies the raw value of DependentStat by a value and adds it to the final TargetStat value.  
eg. `TargetStat + DependentStat * 0.5`

### ConvertedTo
Multiplies the raw value of DependentStat by a value and adds it to the final TargetStat value.  
The DependentStat will be reduced by the same amount. 
eg. `TargetStat + DependentStat * 0.5`

{: .note }
You cannot convert more than 100% of a StatType, all conversion modifier will be scaled down if their cumulative value exceeds 100%.

### ModifiersAlsoApplyToStat


### ConvertSelfTags


### ConvertTargetTags


### FinalAdd


### FinalSumMultiply


### FinalSumMultiply


## Order of operations for Stat calculation
Stat calculations happen in the following order:
1. All 'Add' Modifiers are summed together.
2. Starting with a value of 1, all 'SumMultiply' Modifiers are added. The result is multiplied by the previous value.
3. Starting with a value of 1, all 'ProductMultiply' Modifiers are multiplied. The result is multiplied by the previous value.
4. Any conversions or additions to the StatType are then added to the previous value.
5. Any conversions from the StatType are then remove from the previous value.
6. A final value is randomised between the min and max raw value.
7. PostProcessing 1 is applied to the final value
8. 'Final' type modifiers are applied to the final value
9. PostProcessing 2 is applied to the final value.