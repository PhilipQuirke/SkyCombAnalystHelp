# [SkyComb Analyst - Drone](https://github.com/PhilipQuirke/SkyCombAnalystHelp/) 

# Overview
This ReadMe covers drone flight logs, video metadata, ground elevation, etc. 
(Refer [ReadMe](./README.md) for an overview of the whole application.)
These data sources have variable accuracy, built-in limitations and sometimes outright errors. 

The source code folder DroneSpace folder of the SkyComb Analyst application covers these topics as well.
The application implements a variety of algorithms and cross-checks to minimise the impact of inaccuracies.

# Drone Input
SkyComb Analyst can be used on a single thermal video file, but is most useful when provide with:
- A thermal video file and the corresponding drone flight log - a text file of location and altitude etc information, or
- Paired thermal and optical video files each with its own drone flight logs (so 2 videos and 2 flight logs). Recommended

For example, the Mavic 2 Enterprise (M2E) Dual drone, in a single flight can generate 4 files concurrently:
- DJI_0053.mp4		Optical (aka visible-light) camera video
- DJI_0053.srt		Drone flight log (location, speed, altitude, orientation, fstop, focal length, etc) for optical video
- DJI_0054.mp4		Thermal (aka IR) camera video, for the same time span as the optical video
- DJI_0054.srt		Drone flight log (location, altitude, orientation, color palette) for thermal video
The format of the two flight logs differ somewhat.


# Height vs Altitude vs Elevation
It is important to understand the difference between these terms:
- Drone Height: The height of the drone above the GROUND where it started its flight.
- Drone Altitude: The height of the drone above the SEA LEVEL.
- Ground Elevation: The height of the ground above the SEA LEVEL.
- Surface Elevation: The height of the tree tops above the SEA LEVEL.
The SkyComb Analyst application uses these terms consistently.

For example, a drone placed on the ground in front of you, and switched on, 
will say that the drone is at a height of 0.0 meters, but at an altitude of say 56.4 meters.


# Input Accuracy

## Video Start Time Accuracy
Despite the timestamps of the thermal and optical videos being identical, the 2 video file may NOT start at exactly the same time. 
When the two videos are viewed side by side, there may be a say 0.5 time difference, most visible when the drone turns a corner.

Each thermal video image has little data, and requires no post-processing, so it can be saved to the video file immediately. 
Each optical video frame contains a lot of data, and has to be post-processed (compressed) into MP4 format before it can be saved to the media file.
This is likely why there is a visual delay between the thermal & optical videos.

SkyComb Analyst works better when the videos are time-synchronised.
The SkyComb Analyst UI has a "Video Delay (Secs)" setting to specify the time difference between the two video files. 
(In the source code this is the ThermalToOpticalVideoDelayS setting.)
To evaluate this setting for your video, load your video, set Video Delay to 0 in the UI, set Run Speed to Slow, click Run, 
and as the drone turns a sharp corner, see if the thermal and optical videos start to turn at difference times. 
If they do, modify Video Delay and click Run again, until the videos sync up.
This setting will be saved to the xls. If you reload the video in SkyComb Analyst later, the setting  will be loaded from the xls.

## Drone Flight Log Accuracy
The video and flight log file are time synchronized.

However the data in each "paragraph" of the flight log comes from multiple subsystems.
Those subsystems are not time-synchronized. Some subsystems take longer to evaluate than others (e.g. GPS coordinates) and so are calculated less frequently. 
The data in each paragraph of the flight log is just what data was available at that moment to output to the flight log. 
Some of the data in each paragraph (perhaps GPS) may be older (aka staler) than the other data in the paragraph. SkyComb Analyst copes with this.

## Drone Pitch, Roll & Yaw Accuracy
Drones use internal accelerometers to evaluate their pitch, roll and yaw every so often (not every video frame).
These intermitent evaluations can give small sudden "jumps" in the Pitch, Yaw & Roll values. 
These "steps" can be seen in the xls graphs, when looking at just a few seconds of flight. 
In reality, the drone is moving smoothly in 3 dimensions. SkyComb Analyst automatically smooths this data. 
(In the source code this is the SmoothSectionSize setting.)

This image shows no smoothing (value 0), good smoothing (value 6), and bad over-smoothing (value 12) for part of a flight:
![Smooth Location Sections Example](./Static/SmoothLocationSectionsExample.png?raw=true "Smooth Location Sections Example")
A SmoothSectionSize of 6 corresponds to smoothing over 1.5 seconds of drone flight.

## Drone Gumbal interactions with Pitch, Roll & Yaw
The drone continuously makes small changes in pitch & roll to compensate for small gusts of wind to keep the drone on the path, or to slow down or speed up the drone. 

The drone camera are mounted on a "gimbal" that can move independently of the drone. The gimbal automatically compensates for small changes in pitch, roll & yaw. This gives a much smoother video image. 

When a drone "turns a corner", the camera gimbal compensates for (aka negates) the initial small yaw values for say 1/2 a second, before the yaw increases sufficiently that gimbal realises that the drone is cornering. The camera gimbal will then center and wait for the drone to stop yawing (aka turning). This explains why, as the drone turns a corner, the flight path map shows the drone yawing a 1/2 second before the video image visually begins to show the same yaw.

Note that the pitch, roll & yaw are measured on the drone body (not the gimbal). 

## Drone Location Accuracy
Drones use GPS to evaluate their location as longitude and latitude - but only recalculate the location every second or so.
In between GPS recalculations, the drones use internal accelerometers to estimate the drone location at each video frame.
GPS locations are not 100% accurate, so after each recalculation, the drone location may appear to "jump" a small distance.
		
This image shows the flight path of a drone travelling south (top to bottom). The horizontal "jumps" are caused by a 
GPS recalculation suddenly changing the estimated  drone location by 12cm:
![GPS Location Jump Example](./Static/GpsLocationJumpExample.png?raw=true "GPS Location Jump Example")

SkyComb Analyst smooths out these "jumps" automatically. 

## Drone Altitude Accuracy
Drones evaluate their altitude using air pressure measuring devices called barometers. 
They may also use GPS but while GPS is very accurate for longitude and latitude is is not accurate for altitude.
Generally drones do not give accurate altitude readings. Indeed the readings can be very inaccurate. 
A sample drone flight at sea level in New Zealand recorded a starting altitude of NEGATIVE 75 metres, rising to a value of NEGATIVE 59 metres. The same flight recorded a starting HEIGHT of 0 metres, rising to 16 metres.

If the drone video recording starts and ends at ground level, SkyComb Analysts can partially correct the altitude inaccuracies.
The SkyComb Analyst UI has a "On ground at" setting to specify whethe the video started &/or ended at ground level. 
Refer [Usage](./Usage.md) for more detail on this.

# Drone Overall Data Accuracy
The drone's flight log input may have 60 datums per second (mirroring 60 video frames per second).
For most drone, flight log attributes (including the key location, altitude, pitch & yaw attributes)
are NOT recalculated every frame - instead they are recalculated periodically - introducing error. 

In fact, every data attribute the drone logs has some level of embedded error - from small to large.
SkyComb Analyst uses a variety of methods to automatically minimise these errors.

Human input is needed to minimise some other types of error.
Specifically, the "Video Delay (Secs)", "Flight Delay (Secs)", and "On ground at" settings help minimise errors.

Overall, the drone mid-flight altitude remains the data measurement with the largest error. 

# Camera Gimbal Down Angle
On a drone, the camera gimbal controls where camera is pointing. 
The drone cameras can be adjusted from point horizontally (aka 0 degrees) to point vertically downwards (aka -90 degrees).
The drone camera angle, together with the drone height above ground, are important for converting the drone location to the video image location and coverage.

For the M2E Dual, camera angle is not provided in the flight log data. 
The FlightConfig.cs setting CameraDownAngle provides the default camera down angle for the drone. The setting is a positive number in degrees. 
So for a camera gimbal set at -80 degrees, CameraDownAngle is set to 80.

A camera gimbal setting of -90 degrees (physically pointing straight down) is recommended, 
as it minimises the impact when drone is too high above the trees, or the altitude or elevation data is inaccurate. Else -80 or -75.


# Source Code Terminology
The source files use this terminology:
- Drones make FLIGHTs, at an ALTITUDE, with each flight being subdivided into 0.25 second SECTIONS.
- Drones take THERMAL and OPTICAL videos in flight. Each VIDEO is made up of many FRAMES (aka images).
- The GROUND has an ELEVATION. Trees have a topmost SURFACE some meters above the ground.  


# Source Code
The source files in the DroneSpace folder are:
- Video.cs: Thermal and optical video metadata. Does NOT process the video images.
- FlightSection.cs: Drone flight section raw data (altitude, location, etc). 
- FlightStep.cs: Drone flight path data (speed, etc) derived from FlightSection and Ground data  
- FlightLeg.cs: Segments of the drone flight path that are at a mostly constant altitude, in a mostly constant direction.
- DroneData.cs: Contains all in-memory data we hold about a drone flight, the videos taken, the flight log, and ground DEM and DSM elevations. 
- FlightConfig.cs: Contains configuration settings e.g. ThermalToOpticalVideoDelayS, SmoothSectionSize, ExcludeMarginRatio

## Legs
Most of the drone flight path is categorised as "legs". Each leg is a path with a mostly constant altitude, in a mostly constant direction. 
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


# Drone Specifics 
Each manufacturer's drones needs unique configuration settings

## ExcludeMarginRatio
For many drones the thermal and optical videos have different pixel resolution and horizontal field of vision (HFOV).
SkyComb Analyst shows the location of significant objects found in thermal video on top of the optical video.
So it needs to know the difference between the HFOV of the thermal and optical videos.

Currently this information is provided via the configuration setting ExcludeMarginRatio.
ExcludeMarginRatio is the "margin" of the optical video that is not displayed in the thermal video, as a ratio between 0.0 and 0.5.
The ratio can be manually calculated by comparing images from the thermal and optical cameras "side by side" in the SkyComb Analyst UI.

(ToDo: Auto-calculate ExcludeMarginRatio from the drone manufacturer's published thermal and optical HFOVs)

## Mavic 2 Enterprise Dual 
For a Mavic 2 Enterprise (M2E) Dual drone:
- Flight speed smoothing works well with SmoothSectionSize=5  
- Scaling thermal to optical image works well with ExcludeMarginRatio=0.125. So we exclude a 1/8th margin - both horizontally and vertically. 
- Time between thermal and optical video start (ThermalToOpticalVideoDelayS) differs per video   



