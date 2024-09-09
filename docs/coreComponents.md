---
layout: default
title: Configuration Components
nav_order: 3
---


## DeepStats Core Components

### Configuration Components

[StatConfiguration](components/statConfiguration.md)  
Where you define your Stat types, and Tags and Scalers for your Modifiers and generate the code.

[StatProperties](components/statProperties.md)   
Where you add any post-processing functions to the raw stat values to obtain final values.

[DeepStatsManager](components/deepStatsManager.md)  
A GameObject in the Scene where you set the StatConfiguration and active StatProperties. This is required for DeepStats to function.

### Runtime Components

[DeepStats](components/deepStats.md)  
The core of the library, this is where Modifiers are collected and Stats are calculated. Add this to any instance that needs Stats or is a source of Stats
