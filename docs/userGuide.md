---
layout: default
title: User Guide
nav_order: 2
has_children: true
---

# User Guide

Before starting, it is recommended to read the (Core Concepts)[/coreConcepts.md] as these will make understanding other components of the library easier.

Otherwise, these are the main components
1. StatConfiguration - Where you define your Stat types, and Condition types and Scaler types for Modifiers.
2. StatProperties - Where you define default values for your Stats, and any post-processing functions for the final values
3. DeepStatsManager - A GameObject in the Scene where you set the active StatProperties
4. DeepConditions - A class you can add to any unit that may get affected by Modifier Conditions or Scalers
4. DeepStats - The core of the library, this is where Modifiers are collected and Stats are calculated. Add this to any instance that needs Stats or is a source of Stats