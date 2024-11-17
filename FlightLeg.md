# [SkyComb Analyst](https://github.com/PhilipQuirke/SkyCombAnalystHelp/blob/main/README.md) - Flight legs

## Overview
SkyComb works best with a "grid search" pattern, where the drone mostly flies in straight "legs".

## Flight Leg
A "Flight Leg" is a drone flight path that is mostly at a constant altitude, in a mostly constant direction. Specifically, a leg is a section of a drone flight where:

- The drone is travelling in a constant direction 
- The drone flight path is at a constant height or is slowing and smoothly changing height. 
- The flight section has a duration of at least 5 seconds
- The drone is not pitching up (to decrease forward speed), pitching down (to increase forward speed), cornering or spinning.

## Data Accuracy
The height, location, etc data recorded by the drone is more accurate during Flight Legs.
That is Flight Legs reduce the inaccuracies the drone data.

## Processing
SkyComb needs as much accuracy as possible. 
For this reason, SkyComb only processes the drone video and so only detects animals during Flight Legs.
Hence a drone "grid search" pattern maximises the portion of the flight that SkyComb processes. 

## Filtering
Filters on the main page of SkyComb Analyst allow the user to select which Flight Leg(s) to view and/or process. 
The user can Click a Leg button to select it. 
The user can Shift-Click another Leg button to select a range of Legs.
The user can Ctrll-Click a selected Leg button to de-select it.
The user can only select a contiguous sets of legs. That is they can select D to G but not D, E and G (skipping Leg F). 
