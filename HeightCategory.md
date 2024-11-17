# [SkyComb Analyst](https://github.com/PhilipQuirke/SkyCombAnalystHelp/blob/main/README.md) - Height Categories

## Overview
The height above ground of animals detected by SkyComb are measured in meters (m).
This height above ground data is categorised into 7 height classes to make it easier to understand.

## Top Surface
SkyComb always sees the top surface of an animal. 
For a standing cow, the top surface is their spine/back, and this will be ~1.5m above the ground. 

## Height Categories
SkyComb height categories are based on "building floors": G, 1f, 2f, 3f, 4f, 5f, 6f+ where each "floor" is 3 meters high.

Height "G" covers animals that are between 0 and 3 meters off the ground. 
Height "1" covers animals that are between 3 and 6 meters off the ground, etc. 

An additional height category "?" is used when SymComb can not calculate an animal's height above ground. 

## Height Histogram
After a video has been processed, and animals have been detected, 
a histogram of the number of animals per size height is shown.

## SkyComb Analyst Height Filter
After a video has been processed, and animals have been detected, 
filters on the main page of SkyComb Analyst allow the user to select a range of heights to focus on.
