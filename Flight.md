# [SkyComb Analyst](https://github.com/PhilipQuirke/SkyCombAnalystHelp/blob/main/README.md) - Flight Recommendations 


## Overview
The SkyComb Analyst tool helps environmentalists, conservationists & scientists use a thermal drone as a scientific tool.

The primary use case is a drone with thermal and optical cameras, flying over wilderness, detecting animals. 
This document outlines how best to fly your drone to collect high quality data for this use case.

**Disclaimer**: This page does not tell you how to fly your drone. We assume you already know how to fly your drone. Your drone's safety is your responsibility.


## Recommendations
Here are several recommendations on how to fly data collection missions, to optimse detection of 
animals in a **repeatable, robust, safe** way. Each recommendation is explained in detail later, but in summary they are:
- Decide whether to fly the data collection mission during the Day, at Dusk, at Dawn or at Night.
- Decide on the best/safest height above the surface, and test it.
- Pre-prepare and use programmed flight paths.  
- Test the programmed flight plan fully before the data collection flight.
- Turn on flight log creation
- Use GPS mode
- Start and end video recording when the drone is on ground.
- For most of the flight, fly in straight lines.
- For most of the flight, have the video cameras pointing down.
- Display the thermal video in gray scale
- Use the thermal camera "High Gain" mode
 
The SkyComb Analyst tool works best when these recommendations are followed.


## Safety first
Drones are expensive and somewhat fragile. This tool's authors are risk adverse.
These recommendations balance good animal detection outcomes with keeping the drone safe.

One drone was hurt in the development of this tool (when we ignored the below recommendations).

**Disclaimer**: These recommendations minimise but do not eliminate the risks of data collection. Your drone is your responsibility.


## Fly mostly in straight lines
Drones are unstable flying platforms with a lot of wobble / error in the data they produce. 
Flying at a steady speed, in a steady direction, at a steady height reduces some of these errors.
When the SkyComb Analyst tool detects that the drone is flying a **Leg** (steady speed, direction & height), 
it automatically uses statistical techniques to reduce the error further.
Flight paths containing several long legs are recommended.

![Drone Flight Path Example](./Static/DroneFlightPathExample.png?raw=true "Drone Flight Path Example")

We recommend a "grid search" path like the one on the left - this maximises the area covered. The path on the right is pretty.

## Decide on the best/safest height above the surface
Drone thermal cameras have a lower resolution than their optical camera.
Fly too high and the thermal camera will not have the resolution to detect small animals.
Fly too low and you risk hitting a tree.
Flying 10 meters above the highest tree top in your flight area is recommended.

The Lidar tree-top height data provided by the New Zealand government and others is a phenomenal resource, but it can be some years out of date. 
Trees can grow a lot in several years. When it comes to drone height, you can't safely rely on it.

The recommended approach is to do a test flight at the location, use your drone to visual inspect the landscape, 
find the highest tree top in your flight plan area and record its height. 
Later, fly your data collection flight at 10 meters above the highest tree top.


## Day, Dusk, Dawn or Night
If your drone has both thermal and optical cameras:
- The optical camera works well during the day, dawn and dusk, but not at night (due to low light levels).
- The thermal camera works day or night. At night, the landscape is cold, improving the contrast between the landscape and living things.

Depending on the animals you want to collect data on, you may want to flight your data collection mission during the day, at dusk, at dawn or at night:
- **Day-time** missions have the best visiblity and drone safety. But, with the sun shining, day-time thermal videos will sun-warmed rocks, sun reflections off water etc.  
- With good timing, **dusk** missions still have good visibility at the height your drone is flying, and the highest (most dangerous) obstacles can still be illuminated. Water reflections are eliminated but rocks may still be warm.
- With good timing, **dawn** missions have good visibility at the height your drone is flying, with the highest obstacles can illuminated. Water reflections are eliminated. Rocks will have cooled overnight.
- **Night-time** missions are the most dangerous. The drone built in collision avoidance mechanism may not work in darkness. Following the below recommendations of flight planning and testing make night missions safe. 

The SkyComb Analyst authors flew day, dawn, dusk and night missions safely using the below advice. Our one drone crash ocurred when we ignored the recommendations on this page.


## Pre-prepare and use programmed flight paths
Many drones support programmed flight paths. Once programmed, the flight plan can be run end-to-end automatically. 

SkyComb recommends you pre-prepare and use programmed flight paths:
- You can prepare the flight plan at home when you are not under time or weather pressure and have good internet connectivity.
- Programmed flight paths tend to have more, longer and smoother Legs than a manual flight. 
- The same flight plan can be run year after year, allowing an "apples with apples" comparison of the animal population between years.


## Turn on Flight log creation
Ensure that your drone's "Create flight log" (aka Video Caption) setting is switched on, so that your drone will create a flight log whenever your drone is recording a video.  

For a DJI drone, the flight logs are text files with a .SRT suffix. To enable the creation of the .SRT flight logs, in the DJI Go App:
- Choose the MENU option on the right side of the screen for Images and Video
- Choose the Video icon and ensure the file type is .MP4 (not .MOV)
- Choose the Option tool icon and ensure the "Video Caption" setting is *on*
This page also shows how: [Turn On Video Captions](https://dronesgalaxy.com/dji-drones-how-to-turn-on-video-captions/)

With that option turned on, the .SRT files will be saved along with the .MP4 video file on your SD card when you record video during a flight.


## Use GPS Mode
Ensure that your drone's "Use GPS" setting is switched on, so that your drone will record GSP location in the flight log.

For a DJI drone, this video shows how: [Use GPS](https://www.youtube.com/watch?v=p6DL3UzPyzQ)

When you flight your drone, it will then try to synchronise with the GPS satellites and will show "GPS Mode" (or similar) on the controller. 
If the drone *can't* synchronise with the GPS satellites, it may say "ATTI Mode" or "OPTI Mode". In ATTI and OPTI mode, no GPS data is available, so no GPS data is stored in the flight log.


## Start and end video recording when the drone is on ground.
Drones can calculate their **location** accurately, but many drones **can't** calculate their **height** accurately.
(Refer the [Errors](./Errors.md) page for why.)

If your vendor says your drone provides very accurate drone **height** information (say +/- 10cm) great! 

Otherwise, we recommend starting the video recording while the drone is still on the ground, and continuing recording 
during the flight, until the drone is back on the ground, and only then stopping recording. 

Where SkyComb Analyst has access to very-accurate ground elevation data provided by the New Zealand government and others, 
SkyComb Analyst automatically improves drone height data accuracy using the start & end ground location elevations as reference points. 


## For most of the flight have the video cameras pointing down
We recommend that during the data collection Legs of your missions, the camera is pointing downwards.

This is less important when flying over low scrub. When flying over trees, the thermal camera can detect objects under some depth of foliage (depending on density of foliage, temperature of animal, ambient temperature, etc).
A downwards orientation minimises the depth of foliage between the thermal camera and the animal, and increases detection rates.

You can use a straight-down camera angle (aka 90 degrees down angle). 
If your thermal camera has "vertical field of vision" (VFOV) of say 30 degrees, 
then using a camera down angle of 75 degrees means the thermal video can see 75 +/- 15 degrees. 
That is the video covers 65 to 90 degrees.

Modern drones record the direction the camera was pointing, in the flight log, frame by frame. 
Where supported, SkyComb Analyst uses this very useful feature and information.

This very useful feature was introduced in DJI SDK 4.3 and is incorporated into at least these DJI drones:
- DJI Mavic Air 2
- DJI Mavic 2 Pro/Zoom
- DJI Phantom 4 Pro V2.0
- DJI Inspire 2
- DJI Matrice 200 series
- DJI Matrice 600 series

For older / less capable drones, you will need to maintain a steady "camera down angle" during the flight, remember this andgle, and enter this figure into SkyComb Analyst later. 

## Display the thermal video in gray scale
Thermal camera videos can be shown in a number of different display modes. A common mode is "Red is hot".

SkyComb Analyst (currently) needs the thermal camera video to be in "Gray scale" mode - where the image is shown in shades of white (hot) to black (cold).  


## Use the thermal camera "High Gain" mode
Some thermal cameras have (manufacturer specific) settings that allows them to focus on a smaller range of temperatures. 
Choose the range that most closely aligned to animal body temperatures. 

For example, the DJI Mavic 2 Enterprise has a "Gain Mode" setting. 
If this is set to "High" the gray scale image is restricted to temperatures in the range -10C to 140C. 
This setting appears under the "Menu > Spanner (aka Wrench)" area of the DJI Pilot app.


## Test your programmed flight paths
We strongly recommend you test your flight path before your actual data collection mission:
- At the launch site, during the day, when visibility is good, fly the drone upwards manually, and then visually determine a safe height to fly the drone at. Record this height.
- Update the programmed drone flight path to use the recorded safe height.
- Have the drone autonomously "test" fly the full planned flight path, during the day, with the camera pointing **horizontally**, so you can manually monitor the flight for unexpected obstacles, and confirm it is safe to fly this path at this height.
- Do not change the programmed flight path before the data collection mission.

**Warning**: **NEVER** fly a night-time mission that you have not previously fully tested as detailed above.
The authors ignored this rule just once and damaged a drone:
- We had flown a test flight during the daylight, assessed a safe height, etc.
- But between the daytime test flight and night flight, we extended the programmed search pattern to cover more ground to gather more data, under the strong belief that there were no taller trees in the extended area. 
- Our belief was wrong. At 10pm, our drone hit a tall tree. The tree only became visible seconds before impact. We had insufficient time to react. 
- The search for the downed drone had to start immediately, at 10:30pm, while the drone battery still had power and the drone lights would help our search. By good luck, we retrieved the damaged drone from deep grass. The process was stressful, risky, avoidable and costly. 


## Copying data from your drone to your laptop
Back at home, transfer the video and flight log files to your laptop or similar. 
This usually involves connecting your drone to your laptop with a data cable to access the drone internal physical storage.
Copy the drone files to your computer hard-disk as described in the [DroneDataPort](./DroneDataPort.md) page.

Then run the SkyComb Analyst tool on your new data as described in the [UserInterface](./UserInterface.md) page.


## Summary: Flying a Thermal Data Collection Mission Safely
In summary, to minimise risk to the drone, we recommend this process:

1. Plan the mission at home:
	- If possible, select the target area and plan out your flight path before leaving home, when you are not under time pressure. 
	- If possible, program the flight path into the drone, so the drone can fly the path autonomously (rather than be controlled manually).
2. Test at the launch site during the day:
	- At the launch site, during the day, when visibility is good, fly the drone upwards manually, and then visually determine a safe height to fly the drone at. 
	- Update the programmed drone flight path to use the recorded safe height.
	- Have the drone autonomously "test" fly the full planned flight path, during the day, with the camera pointing **horizontally**, so you can manually monitor the flight for unexpected obstacles, and confirm it is safe to fly this path at this height.
3. Collect the real data:
	- Starting from exactly the same launch location as in Step 2, using the same programmed flight path...
	- Start video recording while the drone is on the ground  
	- Have the drone run the same flight path as in step 2, but with the camera pointing **vertically downwards**.
	- Stop video recording only after the drone is back on the ground 
4. Process the data collected at home.
	- Transfer the new videos and flight log files from your drone to your laptop or similar. 
	- Process the new file using the SkyComb Analyst tool as described in the [UserInterface](./UserInterface.md) page.

