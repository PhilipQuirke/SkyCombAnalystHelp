# [SkyComb Analyst - End to End Usage](https://github.com/PhilipQuirke/SkyCombAnalyst/) 


# Overview
SkyComb Analyst helps environmentalists, scientists & software developers make a drone into a scientific tool.
The primary use case is a drone with thermal and optical camera, flying over wilderness, detecting animals. 

This page does NOT cover the mechanics of how to operate a drone. It assumes you know how to fly your drone.

This page outlines the end to end process of how best to:
- Plan and fly a drone mission to collect video and flight log data
- Load that data into SkyComb Analyst and tune the processing of it. 


# Safety first
Drones are expensive and somewhat fragile. 

Thermal cameras work best at night or in low light conditions. Flying a drone in these conditions adds risk. 

The SkyComb Analyst authors have basic drone skills. Despite this, no drones were hurt in the development of this tool and this guide.

The authors are risk adverse. This guide balances obtaining good animal detection outcomes with minimising risk to the drone.


# Flying a Thermal Data Collection Mission Safely
To minimise risks to the drone, we recommend this process:

1. Plan the mission at home:
	- Select the target area and plan out your flight path before leaving home (more on this later)
	- If your drone supports this, program the flight path into the drone, so the drone can fly the path autonomously (rather than be controlled manually).
2. Test at the launch site during the day:
	- At the launch site, during the day, when visibility is good, fly the drone upwards manually, and then visually determine a safe height to fly the drone at. Say 10 to 15 metres higher than the tallest tree in the flight area. Record this height.
	- Update the programmed drone flight path to use the above "proved safe" height.
	- Have the drone autonomously "test" fly the path, during the day, with the camera pointing horizontally, so you can manually monitor the flight for unexpected obstacles, and confirm it is safe to fly this path at this height.
3. Collect the real data before dawn:
	- In the hour before dawn (more on why later), starting from exactly the same launch location as in Step 2, using the same programmed flight path...
	- Start video recording while the drone is on the ground (more on why later)
	- Ensure you (or some other hot object) are visible to the drone video early in the flight (more on why later)
	- Have the drone run the same flight path as in step 2, but with the camera pointing vertically downwards.
	- Stop video recording only after the drone is back on the ground (more on why later)
4. Process the data collected at home.
	- Transfer the new videos and flight log files from your drone to your laptop or similar. 
	- Process the new file using the SkyComb Analyst tool 

## What Path to Fly
There are many ways to design a flight path to collect data:
- If you have a large area to cover, or your target animal is rare, then a "lawn mowing" pattern covers the most land, and collects the most data.   
- If you are focused on a small area, then a "criss cross" pattern will covers the same area multiple times from different directions.

![DroneFlightPathExample](./Static/DroneFlightPathExample.png?raw=true "Drone Flight Path Examples")


## What Time of Day to Fly
If your drone has both thermal and optical cameras:
- The optical camera works well during the day, and not at night (due to low light levels).
- The thermal camera works during the day but better at night. At night, the landscape is cold, improving the contrast between the landscape and living things.

The best option is to fly data collection missions in the hour before dawn, when there is some light in the sky (for the optical camera), 
and the landscape has cooled overnight (helping the thermal camera detect animals).


## Improved Drone Altitude via "On Ground At Start/End"
Drones can calculate their <u>location/u> accurately (using GPS), but calculate their height <u>inaccurately</u>
(using barometers and accelerometers). 

We recommend starting the video recording while the drone is still on the ground, continuing recording 
during the flight, and only stoppng recording after the drone is back on the ground. If you do this, and SkyComb Analyst can use 
alterative sources of highly-accurate ground elevation data to automatically correct  
drone height/altitude accuracy by using the start & end ground location elevations as reference points. 

With the UI setting "On Ground At" you state if the drone flight started/ended on the ground.
As an example, consider the below real drone flight that started and ended on the ground. 
The elevations as measured by the drone were inaccurate at the start (common), inaccurate at the end (common), 
and the inaccuracy varied during the flight (uncommon). This one physical flight is shown four times, 
demonstrating how the four different "On Ground At" settings adjust for the inaccuracies. 

The charts shows the ground elevation in brown, the tree-top height in green and drone altitude in blue. The four settings are:
- <b>Auto</b> : Shows the raw drone data. The red arrows show the "raw" inaccuracies in drone start and end heights.
- <b>Start</b> : Corrects the drone altitude assuming the drone was on the ground at the start (only). This is a partial fix.
- <b>End</b> : Corrects the drone altitude assuming the drone was on the ground at the end (only). This is a partial fix.
- <b>Both</b> : Corrects assuming the drone was on the ground at both the start and end, and gives the best correction. This is the recommended approach.

![On Ground At Examples](./Static/OnGroundAtExamples.png?raw=true "On Ground At Examples")


## Camera Down Angle
We recommend that during your data collection missions, the camera is pointing straight down for the bulk of the flight. 

If the CameraDownDeg is not recorded in the flight log (common), SkyComb Analyst can't automatically detect or calculate the angle. 
You can manually specify the CameraDownDeg value in the UI.

If the camera was pointing straight down, then set CameraDownDeg to 90 (not -90) in the SkyComb Analyst UI.
If the camera was pointing straight forward (horizontally), then set CameraDownDeg to 0.
If the camera was pointing half way between straight down and straight forward, then set CameraDownDeg to 45.  


# Loading data into SkyComb Analyst
Back at home, transfer the video and flight log files to your laptop or similar. 
This usually involves connecting your drone to your laptop with a data cable to access the drone internal physical storage.
Copy the drone files to your computer hard-disk.
Then run the SkyComb Analyst tool and select your new thermal or optical video file (it doesn't matter which one). 

If SkyComb Analyst supports the drone flight log file format, the flight log file will be processed.
If SkyComb Analyst supports the location flown over, detailed ground and tree-top elevations will be loaded from public sources. 

The drone flight path, speed, altitude, etc will be displayed. The ground and tree-top elevations will also be shown.

![UI Sample](./Static/UIExample.png?raw=true "UI Example")

A spreadsheet containing this data and these graphs will be automatically created for further processing.

Some parameters specific to your drone and flight need to be manually tuned. SkyComb Analyst will help you do this.

## Syncing the Drone Thermal and Optical Videos
While you might expect the thermal and optical videos to be automatically time synced, often this is not the case. 

SkyComb Analyst can't automatically detect or calculate this difference (yet!). 
You can calculate the difference manually using SkyComb Analyst and then specify the difference in the UI.

To do this, visually locate the first sharp "corner" early in the flight path shown in the tool. 
Set "From (Secs)" to a few seconds before this time, and "To (Secs)" to a few seconds after this time. 
Set the "Process" to "None". 

Click "Run" again and focus on just the thermal and optical videos. 
If the optical video starts turning roughly a second before the thermal video,
set the "Video delay (Secs)" to "1.0". Run the process again and further tune this 
setting until the two videos are synchronized and turn the corner at the same time.

Each time you click "Run" the settings are saved to the spreadsheet. 
The next time you run SkyComb Analyst and select the same video, 
your settings are automatically loaded from the spreadsheet.


## Tuning the "hot" threshold
Thermal image processing algorithms must look at an image and decide which pixels are "hot" 
and which are "not hot" using a "threshold value". 

SkyComb Analyst can't automatically detect or calculate the "best" ThresholdValue (yet!).
You can calculate the best value using SkyComb Analyst and then record the best value in the UI.

Click "Run" & watch the optical video in SkyComb Analyst, to locate a hot object 
(it could be you) preferably early in the video, and note the time it appears.
In SkyComb Analyst set "From (Secs)" to a few seconds before this time, and "To (Secs)" to a few seconds after this time. 

Set the "Process" to "Threshold" and set "Threshold value" to say "200". Click "Run" and watch the thermal video. 
The thermal image will highlight the pixels that are hotter than this threshold in blue.

Change the "Threshold value" to say "195" and click "Run" again. Try out several higher and lower threshold values. 
The goal is to roughly tune the threshold value until the hot object is painted in blue, while most of the rest of the image is not blue.

Threshold Values as low as 150 and as high as 235 have been seen with various drone thermal videos.


## ThermalToOpticalVideoImageRatio
For many drones the thermal and optical videos have different pixel resolution and horizontal field of vision (HFOV).
SkyComb Analyst shows the location significant objects found in thermal video on top of the optical video.
So it needs to know the difference between the HFOV of the thermal and optical videos.

Currently this information is provided via the configuration setting ThermalToOpticalVideoImageRatio

ToDo: Support tuning of ThermalToOpticalVideoImageRatio
ToDo: Auto-calculate ExcludeMarginRatio from the drone manufacturer's published thermal and optical HFOVs


# Process the whole video
Having configued the above parameters which are specific to your drone and flight, you are ready to process the video.

Set the "Process" to "Comb". Click the "All" Legs button under the flight path widget. Click "Run"


# Supporting More Drone Types
Each drone manufacturer has their own "flight data" file format - often in a human readable text file. 
This format can also differ between different generations of drones from one manufacturer.

Currently SkyComb Analyst only supports DJI Mavic 2 Enterprise and and DJI Mini (2022 model) flight data text 
files, which are named "DJI*.SRT". This DJI-drone-specific is isolated to code in DroneData.cs in the 
function LoadFlightInputFromDjiSrt.

If you want to use a different drone, and can provide sample drone videos and flight data, 
the developers of SkyComb Analyst will extend DroneData.cs to support your drone.
Alternatively, you could extend the code yourself. If you do please push your changes to this repo.


# Accurate Ground Elevation
Accurate ground elevation (height above sea level) data and tree-top elevation data improves the 
SkyComb Analyst tool functionality. Many countries have accurately mapped part or all of their land 
using a technology called Lidar. Many countries provide this data for free.

The SkyComb Analyst tool evaluates ground and tree-top elevation data in Ground.cs in the function 
GlobalCalculateElevations. But there is no one easy source of Lidar covering all the world. So this 
function currently only covers New Zealand. The function is easily extensible. If you need 
a different part of the world supported, tell us, and the SkyComb Analyst creators will try to 
find matching Lidar data and extend the function. Alternatively, you could extend the code yourself. 
If you do please push your changes to this repo.

If SkyComb Analyst can obtain accurate ground elevation data, it will do so automatically, and the 
the ground elevation will be displayed on the altitude chart, and saved to the spreadsheet.
