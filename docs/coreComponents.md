---
layout: default
title: Core Components
nav_order: 3
---


## DeepStats Core Components
StatConfiguration
Where you define your Stat types, and Tags and Scalers for your Modifiers and generate the code.

StatProperties
Where you add any post-processing functions for the final values

DeepStatsManager
A GameObject in the Scene where you set the StatConfiguration and active StatProperties. This is mandatory

DeepConditions
A class you can add to any instance that is affected by Tags or Scalers

DeepStats
The core of the library, this is where Modifiers are collected and Stats are calculated. Add this to any instance that needs Stats or is a source of Stats