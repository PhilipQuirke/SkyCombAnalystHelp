# [SkyComb Analyst](https://github.com/PhilipQuirke/SkyCombAnalystHelp/blob/main/README.md) - Height Categories

## Overview
An animal's height above ground is useful information. Some mammals climb tress while others don't. 
SkyComb measures the height above ground of detected animals in meters (m).

## Top Surface
SkyComb always sees the top surface of an animal. 
For a standing cow, the top surface is their spine/back, and this will be ~1.5m above the ground. 

## Height Categories
The height above ground data is categorised into 7 height classes to make it easier to understand.
Height categories are based on "building floors" and are named G, 1f, 2f, 3f, 4f, 5f, 6f+ 

Each "floor" is 3 meters high. So height "G" covers animals that are between 0 and 3 meters off the ground. 
Height "1" covers animals that are between 3 and 6 meters off the ground, etc. 

An additional height category "?" is used when SymComb can not calculate an animal's height above ground. 
This can occur when an animal is only seen for a brief time. 

## Height Histogram
After a video has been processed, and animals have been detected, 
a histogram of the number of animals per size height is shown.

## SkyComb Analyst Height Filter
After a video has been processed, and animals have been detected, 
filters on the main page of SkyComb Analyst allow the user to select a range of heights to focus on.
