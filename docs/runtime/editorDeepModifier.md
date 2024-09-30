---
layout: default
title: EditorDeepModifier
nav_order: 2
parent: Runtime Classes
---

# EditorDeepModifier
This is the authoring class for creating Modifiers via the Unity Editor. Use it's custom editor to create a wide range of Modifiers. Modifiers can be added to DeepStatsInstances and DeepModifierCollections

## Modifier Overview

![same min max](../../images/modifierOverview.png)

1. Modifier Type: The type of modification to the Stat you want to make.
2. Set Min / Max Values: Whether you'll be modifying the min and max value of the Stat separately.
3. Modify Value: The magnitude to apply this Modifier.
4. Target Stat: Which Stat you want to modify.
5. Modifier Scaling Source: Whether you want to scale the Modify Value. 'Self' will use a Scaler from the DeepStats with this Modifier, 'Target' will use a Scaler from a Target DeepStats passed in when calculating stats. You can also use both, in which case they Scalers will be added together.
6. Modifier Scaler: Which Scaler value to look up.
7. Clamp Scaler Range: The min and max values to clamp the Scaler to.
8. The required Tags on the DeepStats instance that has this Modifier for this Modifier to apply
9. The required Tags on the Target DeepStats instance passed in when calculating stats, for this Modifier to apply.

## Types of Modifiers

### Add
 Adds a flat value to the target stat.  
 eg. `TargetStat + 5`

![same min max](../../images/addModifier.jpg)

### SumMultiply
Adds a value with all the other SumMultiply mods, before multiplying the target stat.  
eg. `TargetStat * (1 + mod1 + mod2 + mod3 + ...)` 

![same min max](../../images/sumMultiplyModifier.jpg)

### ProductMultiply
Multiplies the target stat by a value.  
eg. `TargetStat * 2`

![same min max](../../images/productMultiplyModifier.jpg)

### AddedAs
The base value of Dependent Stat is converted into Target Stat, and then scaled by any Sum/Product Multiplies which affect either the dependent or target Stat Types. The modifiers are combined together before applying so that the standard order of operations still applies. If a chain of AddedAs is created by converting a stat multiple times, the modifiers of any of the relevant stat types apply to the final value.
eg. `DependentStat * 0.5 * (1 + dependentSumMultiplies + targetSumMultiplies) * (dependentProductMultiplies * targetProductMultiplies)`

![same min max](../../images/addedAsModifier.jpg)

### ConvertedTo
ConvertedTo operates the same as AddedAs, except additionally the DependentStat will be reduced by the conversion ratio.  

{: .note }
You cannot convert more than 100% of a Stat. If total conversion exceeds 100%, all conversion Modifiers will be scaled down equally so that the sum is 100%.

![same min max](../../images/convertedToModifier.jpg)

### ModifiersAlsoApplyToStat
Takes the total modifications to each Target Modify Type from Dependent Stat, and accumulates them onto Target Stat.

![same min max](../../images/alsoAppliesToStatModifier.jpg)

### ConvertSelfTags
Finds any Modifiers which have the Required Tags under Self and creates a copy of them with Required Tags replaced by New Tags.

![same min max](../../images/convertSelfTagModifier.jpg)

For example, the Modifier below would have a second version added that requires a Player tag instead of a Minion Tag.

![same min max](../../images/convertSelfTagsModifierExample.png)

### ConvertTargetTags
Functions the same as ConvertSelfTags, except it searches for Tags in the Target section instead.

![same min max](../../images/convertTargetTagModifier.png)

### FinalAdd, FinalSumMultiply, FinalSumMultiply
These operate the same as the non-final Modifier types, except they apply between PostProcessing 1 and 2. They can be used to Modify a Stats' final value.

## Order of operations for Stat Calculation
Stat calculations happen in the following order:
1. All 'Add' Modifiers are summed together.  
2. Starting with a value of 1, all 'SumMultiply' Modifiers are added. The result is multiplied by the previous value.  
3. Starting with a value of 1, all 'ProductMultiply' Modifiers are multiplied. The result is multiplied by the previous value.  
4. Any conversions or additions TO this StatType are then added.  
5. Any conversions FROM the StatType are then removed.  
6. Raw value is now complete.
7. PostProcessing 1 is applied to raw value.  
8. 'Final' type modifiers are applied.  
9. PostProcessing 2 is applied.  
10. Final value is now complete.

## Usage Notes

### EditorDeepModifiers create a DeepModifier value type so they should be treated as immutable.
Once an EditorDeepModifier has been accessed (by reading the `.value` property), it cannot be changed because it builds a struct internally which is what DeepStatsInstances actually use. This generally means that any changes made to an EditorDeepModifier in the inspector during gameplay will not be reflected in the Modifier.

### Always prefer to create Modifiers using the EditorDeepModifier class
You can create DeepModifier structs directly and this will work fine for simple Modifiers, however the editor provides a number of safety checks to ensure your Modifiers are created correctly so should always be preferred.