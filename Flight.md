# [SkyComb Analyst Help - Flight Recommendations](https://github.com/PhilipQuirke/SkyCombAnalystHelp/) 


# Overview
The [SkyComb Analyst](https://github.com/PhilipQuirke/SkyCombAnalyst/) tool 
helps environmentalists, scientists & software developers make a drone into a scientific tool.

The primary use case is a drone with thermal and optical camera, flying over wilderness, detecting animals. 
This document outlines how best to fly your drone to collect high quality data for this use case.

To understand how to use the collected afterwards in SkyComb Analyst please refer to the [UserInterface](./UserInterface.md) page.


# Recommendations
The SkyComb Analyst tool supports collecting data on animal populations in a **repeatable, robust, safe** way.
Aligned to this goal, this page contains several recommendations on how to fly data collection missions.
Each is explained in detail below, but in summary the recommendations are:
- Fly in straight lines.
- Decide on the best height above the surface.
- Decide whether to fly during the Day, at Dusk, at Dawn or at Night.
- Start and end video recording when the drone is on ground.
- For most of the flight have the video cameras pointing straight down.
- Record the thermal video in gray scale (not say in a "red is hot" mode).
- Pre-prepare and use programmed flight paths. (Don't fly the drone manually when collecting data).
- Test flight plans fully before the data collection flight

**Disclaimer**: This page does not tell you how to fly your drone. We assume you already know how to fly your drone. Your drone is your responsibility.


# Safety first
Drones are expensive and somewhat fragile. The authors are risk adverse. These recommendations balance good animal detection outcomes with protecting the drone.

The SkyComb Analyst authors have basic drone skills. One drone was hurt in the development of this tool (when we ignored the below recommendations).

**Disclaimer**: These recommendations minimise but do not eliminate the risks of data collection. Your drone is your responsibility.


# Fly in straight lines lots
Drones are unstable flying platforms with a lot of wobble / error in the data they produce. 
Flying at a steady speed, in a steady direction, at a steady height reduces some of these errors.
When the SkyComb Analyst tool detects that the drone is flying a **Leg** (steady speed, direction & height), 
it uses statistical techniques to reduce the error further.
Flight paths containing several long legs are recommended.

![Drone Flight Path Example](./Static/DroneFlightPathExample.png?raw=true "Drone Flight Path Example")


# Decide on the best height above the surface
Drone thermal cameras have a lower resolution than their optical camera.
Fly too high and the thermal camera will not have the resolution to detect small animals.
Fly too low and you risk hitting a tree.
Flying 10 meters above the highest tree top in your flight area is recommended.

The tree-top height data provided by say the New Zealand government is a phenomenal resource, but it can be several years out of date. 
Trees can grow a lot in several years. When it comes to drone safety, you can't rely on it.

The best approach is to do a test flight at the location, use your drone to visual inspect the landscape, 
find the highest tree top in your flight plan area and record its height. Fly your data collection flight at 10 meters above the highest tree top.




TBC

Many drones have built in collision avoidance mechanisms. These mechanisms may only work when the drone is moving at low speed, and may only work when there is sufficient light to see obstacles. Be aware of the limitations of your drone. 


# Day, Dusk, Dawn and Night
Depending on the animals you want to collect data on, you may want to flight your drone to collect data during the day, at dusk, at dawn or at night:
- Day-time missions have the best visiblity
- Missions at Dusk and Dawn may have good visibility at the height your drone is flying, and the highest (most dangerous) obstacles are generally illuminated first.
- Missions at Night are by far the most dangerous. The drone built in collision avoidance mechanism may not work in darkness.

The SkyComb Analyst authors flew day, dawn, dusk and night missions safely using the below advice. The one crash we had was where we ignored the below advice. 


# What Time of Day to Fly
If your drone has both thermal and optical cameras:
- The optical camera works well during the day, dawn and dusk, but not at night (due to low light levels).
- The thermal camera works day or night. At night, the landscape is cold, improving the contrast between the landscape and living things.

The best option is to fly in the hour before dawn, or around dusk when there is some light in the sky (for the optical camera), 
and the landscape has cooled overnight (helping the thermal camera detect animals).

Flying at other times of day may still work well enough.


# Flying a Thermal Data Collection Mission Safely
To minimise risks to the drone, we recommend this process:

1. Plan the mission at home:
	- If possible, select the target area and plan out your flight path before leaving home, when you are not under time pressure. 
	- If possible, program the flight path into the drone, so the drone can fly the path autonomously (rather than be controlled manually).
2. Test at the launch site during the day:
	- At the launch site, during the day, when visibility is good, fly the drone upwards manually, and then visually determine a safe height to fly the drone at. Say 10 to 15 metres higher than the tallest tree in the flight area. Record this height.
	- Update the programmed drone flight path to use the recorded safe height.
	- Have the drone autonomously "test" fly the full planned flight path, during the day, with the camera pointing **horizontally**, so you can manually monitor the flight for unexpected obstacles, and confirm it is safe to fly this path at this height.
3. Collect the real data:
	- Starting from exactly the same launch location as in Step 2, using the same programmed flight path...
	- Start video recording while the drone is on the ground (more on why later)
	- Ensure you (or some other hot object) are visible to the drone video early in the flight (more on why later)
	- Have the drone run the same flight path as in step 2, but with the camera pointing **vertically downwards**.
	- Stop video recording only after the drone is back on the ground (more on why later)
4. Process the data collected at home.
	- Transfer the new videos and flight log files from your drone to your laptop or similar. 
	- Process the new file using the SkyComb Analyst tool as described in the [UserInterface](./UserInterface.md) page.

**Warning**: **NEVER** fly a night-time mission that you have not previously fully tested when visibility was good (point 2 above). 
The authors ignored this rule just once and damaged a drone:
- We had flown a test flight during the daylight, assessed a safe height, etc.
- But between the daytime test flight and night flight, we extended the programmed search pattern to cover more ground to gather more data, under the strong belief that there were no taller trees in the extended area. 
- Our belief was wrong. At 10pm, our drone hit a tall tree. The tree only became visible seconds before impact. We had insufficient time to react. 
- The search for the downed drone had to start immediately, at 10:30pm, while the drone battery still had power and the drone lights would help our search. We retrieved the damaged drone as much by luck as by good management. The process was stressful and risky and was avoidable. 


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
