# [SkyComb Analyst](https://github.com/PhilipQuirke/SkyCombAnalystHelp/blob/main/README.md) - Drone

## Overview
This ReadMe covers the purpose and content of the DroneSpace folder of the SkyComb Analyst application.
(Refer the root-level [ReadMe](./ReadMe.md) for an overview of the whole application.)
DroneSpace covers drone flight logs, video metadata, ground elevation, etc. Also the Drone source code.


## Out of Scope
This page does <u>not</u> cover:
- How to fly your drone. We assumes you already know how to fly your drone.
- How to prepare for and run drone data collection flights. Refer [Flight](./Flight.md) page.
- How to use the SkyComb Analyst tool to analyse the data collected. Refer [UserInterface](./UserInterface.md)
- The inaccuracies inherent in drone flight log data. Refer [Errors](./Errors.md) page.
- How to copy video and flight log files from your drone. Refer [DroneDataPort](./DroneDataPort.md) page.


## Drone Input
SkyComb Analyst can be used on a single thermal video file, but is most useful when provide with:
- A thermal video file and the corresponding drone flight log - a text file of location and altitude etc information, or
- Paired thermal and optical video files each with its own drone flight logs (so 2 videos and 2 flight logs).

For example, the Mavic 2 Enterprise (M2E) Dual drone, in a single flight can generate 4 files concurrently:
- DJI_0053.mp4		Optical (aka visible-light) camera video
- DJI_0053.srt		Drone flight log (location, speed, altitude, orientation, fstop, focal length, etc) for optical video
- DJI_0054.mp4		Thermal (aka IR) camera video, for the same time span as the optical video
- DJI_0054.srt		Drone flight log (location, altitude, orientation, color palette) for thermal video
The format of the two flight logs differ somewhat.

The [DroneDataPort](./DroneDataPort.md) page explains how to copy video and flight log files from your drone to your computer.


## Height, Altitude & Elevation terminology
It is important to understand the difference between these terms:
- Drone Height: The height of the drone above the GROUND where it started its flight.
- Drone Altitude: The height of the drone above the SEA LEVEL.
- Ground Elevation: The height of the ground above the SEA LEVEL.
- Surface Elevation: The height of the tree tops above the SEA LEVEL.
The SkyComb Analyst application uses these terms consistently.

For example, when you place a drone on the ground in front of you, and switch it on, 
the drone will say that it is at a height of 0.0 meters, but at an altitude of say 56.4 meters.

The source files use this terminology:
- Drones make FLIGHTs, at an ALTITUDE, with each flight being subdivided into 0.25 second SECTIONS.
- Drones take THERMAL and OPTICAL videos in flight. Each VIDEO is made up of many FRAMES (aka images).
- The GROUND has an ELEVATION. Trees have a topmost SURFACE some meters above the ground.  


## Legs
Much of the drone flight path is usually what is termed "legs". 
Each leg is a path with a mostly constant altitude, in a mostly constant direction. 
Each leg is independent (non-overlapping) of the other legs.

Specifically, a leg is a section of a drone flight that:
- Is a level flight i.e. has a constant Altitude within +/- 2 meters
- Is in a constant direction i.e. has a DeltaYawRad of less than 0.2 over leg
- Is not pitching up (to slow down) or pitching down (to speed up).
- Has a duration of at least 5 seconds 
- Travels at least 5m horizontally.    
- Does not contain a flight data gap of 0.5 seconds or more. (This is a rare case where the flight log data is missing data for that period.)
These criteria threshold values are defined in FlightConfig.cs

Parts of the flight path that are NOT part of any leg include spinning (changing direction), hovering (not moving), climbing or descending.


## Supporting More Drone Types
Each drone manufacturer has their own "flight data" file format - often in a human readable text file. 
This format can also differ between different generations of drones from one manufacturer.

Currently SkyComb Analyst only supports DJI Mavic 2 Enterprise and and DJI Mini (2022 model) flight data text 
files, which are named "DJI*.SRT". This DJI-drone-specific is isolated to code in DroneAll.cs in the 
function LoadFlightInputFromDjiSrt.

If you want to use a different drone, and can provide sample drone videos and flight data, 
the developers of SkyComb Analyst will extend DroneAll.cs to support your drone.
Alternatively, you could extend the code yourself. If you do please push your changes to this repo.
