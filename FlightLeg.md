# [SkyComb Analyst](https://github.com/PhilipQuirke/SkyCombAnalystHelp/blob/main/README.md) - Flight legs

## Overview
SkyComb is most accurate when the drone flies in a "grid search" pattern. That is the drone flies in straight "legs" most of the time as shown in this example.

![DroneFlightPathForm](./Static/DroneFlightPathForm.png?raw=true "DroneFlightPathForm")

## Flight Leg
A "Flight Leg" is a drone flight path that is mostly at a constant altitude, in a mostly constant direction. More specifically:

- The drone is travelling in a constant direction 
- The drone flight path is at a constant height or is slowing and smoothly changing height. 
- The flight section has a duration of at least 5 seconds
- The drone is not pitching up (to decrease forward speed), pitching down (to increase forward speed), cornering or spinning.

## Data Accuracy
During flight legs, the momentum of the drone helps keep the path steady. 
While gusts of wind can rock the drone, the height, location, etc data recorded by the drone are more accurate during Legs than at other times.
That is Flight Legs reduce the inaccuracies in the drone data, and so increase the accuracy of the SkyComb results

## Processing
SkyComb needs as much accuracy as possible. 
For this reason, SkyComb only processes the drone video and so only detects animals during Flight Legs.
Hence a drone "grid search" pattern maximises the portion of the flight that SkyComb processes. 
In the above image, the flight corners are not processed and so show as a thin blue line, while the legs show as a thick blue line, and is labelled with a letter.

## Filtering
On the main page of SkyComb Analyst, the legs are shown as button (e.g. "A" to "K"). 
These buttons allow the user to select which Flight Leg(s) to view and/or process.

The user can Click a Leg button to select it. 
The user can Shift-Click another Leg button to select a range of Legs.
The user can Ctrl-Click a selected Leg button to de-select it.
The user can only select a contiguous sets of legs. That is they can select D to G but not D, E and G (skipping Leg F). 
