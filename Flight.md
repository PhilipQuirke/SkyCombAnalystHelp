# [SkyComb Analyst Flight](https://github.com/PhilipQuirke/SkyCombAnalyst/) 


# Overview
SkyComb Analyst helps environmentalists, scientists & software developers make a drone into a scientific tool.
The primary use case is a drone with thermal and optical camera, flying over wilderness, detecting animals. 
This document outlines how best to fly your drone to collect high quality data.


# Out of Scope
This page does **not** cover:
- How to actually fly your drone. We assumes you already know how to fly your drone.
- How to use the SkyComb Analyst tool to analyse the data collected. Refer [UserInterface](./UserInterface.md)
- The inaccuracies inherent in drone flight data. Refer [Errors](./Errors.md) page.


# Safety first
Drones are expensive and somewhat fragile. 

Thermal cameras work best at night or in low light conditions. Flying a drone in these conditions adds risk. 

The SkyComb Analyst authors have basic drone skills. Despite this, no drones were hurt in the development of this tool and this guide.

The authors are risk adverse. This guide balances obtaining good animal detection outcomes with protecting the drone.


# Flying a Thermal Data Collection Mission Safely
To minimise risks to the drone, we recommend this process:

1. Plan the mission at home:
	- Select the target area and plan out your flight path before leaving home. 
	- If possible, program the flight path into the drone, so the drone can fly the path autonomously (rather than be controlled manually).
2. Test at the launch site during the day:
	- At the launch site, during the day, when visibility is good, fly the drone upwards manually, and then visually determine a safe height to fly the drone at. Say 10 to 15 metres higher than the tallest tree in the flight area. Record this height.
	- Update the programmed drone flight path to use the recorded safe height.
	- Have the drone autonomously "test" fly the path, during the day, with the camera pointing horizontally, so you can manually monitor the flight for unexpected obstacles, and confirm it is safe to fly this path at this height.
3. Collect the real data before dawn:
	- In the hour before dawn (more on why later), starting from exactly the same launch location as in Step 2, using the same programmed flight path...
	- Start video recording while the drone is on the ground (more on why later)
	- Ensure you (or some other hot object) are visible to the drone video early in the flight (more on why later)
	- Have the drone run the same flight path as in step 2, but with the camera pointing vertically downwards.
	- Stop video recording only after the drone is back on the ground (more on why later)
4. Process the data collected at home.
	- Transfer the new videos and flight log files from your drone to your laptop or similar. 
	- Process the new file using the SkyComb Analyst tool as described in the [UserInterface](./UserInterface.md) page.


# What Time of Day to Fly
If your drone has both thermal and optical cameras:
- The optical camera works well during the day, and not at night (due to low light levels).
- The thermal camera works day or night. At night, the landscape is cold, improving the contrast between the landscape and living things.

The best option is to fly in the hour before dawn, when there is some light in the sky (for the optical camera), 
and the landscape has cooled overnight (helping the thermal camera detect animals).

Flying at other times of day may still work well enough.


# Improved Drone Altitude via "On Ground At Start/End""
Drones can calculate their **location** accurately (using GPS), but calculate their height **inaccurately**
(using barometers and accelerometers). For more detail refer to the [Errors](./Errors.md#drone-altitude-vs-height) page.

We recommend starting the video recording while the drone is still on the ground, and continuing recording 
during the flight, until the drone is back on the ground. If you do this, and SkyComb Analyst has access to 
alterative highly-accurate ground elevation data then SkyComb Analyst can improve 
drone height/altitude accuracy using the start & end ground location elevations as reference points. 


# Camera Down Angle
We recommend that during your data collection missions, the camera is pointing straight down for the bulk of the flight. 

This camera angle gives the best accuracy when SkyComb Analyst needs to calculate the height above ground of objects detected.


# Copying data from your drone to your laptop
Back at home, transfer the video and flight log files to your laptop or similar. 
This usually involves connecting your drone to your laptop with a data cable to access the drone internal physical storage.
Copy the drone files to your computer hard-disk.

Then run the SkyComb Analyst tool on your new data as described in the [UserInterface](./USerInterface.md) page.
