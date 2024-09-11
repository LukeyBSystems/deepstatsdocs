Welcome to the public DeepStats repository.

Find the documentation at:
https://lukebolly.github.io/deepstatsdocs/

TODO list:
- Add a warning in the modifier property drawer when a backwards stat dependency is added (eg. Health declared before Armour, but modifier converts Armour to Health)
- Add a ModifyType which allows converting some modifiers to others (eg. increases to fire damage also apply to ice damage)
- Add a ModifyType which allows modifying Conditions / Scalars (eg. a Secondary DeepConditions are calculated so we can have Modifiers like 'Modifiers to Swords also apply to Maces')