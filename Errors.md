# [SkyComb Analyst Error Sources](https://github.com/PhilipQuirke/SkyCombAnalyst/) 


# Overview
The SkyComb Analyst tool helps environmentalists, scientists & software developers make a drone into a scientific tool.

A key technical goal in the creation of this tool was to minimise the negative impact of various sources of error. 
This document outlines these sources of error & how SkyComb Analyst minimses them. 


# Drone Overview
A drone is a complex collection of multiple sub-systems (motors, accelerometers, video cameras, camera gimbal, GPS etc). 
Each sub-system provides data and each has its own error source(s).
The drone must integrate these data feeds, make and execute decisions, and store selected data as videos and flight logs - all in real-time.

This document is not a critique of drones or drone engineers. It is instead a survery of real world error sources.


# Drone Location

## Drone Location Terminology
Drones usually obtain their location from GPS data and record the location data as 
[Longitude & Latitude](https://en.wikipedia.org/wiki/Geographic_coordinate_system#Latitude_and_longitude) coordinates.
For example, in New Zealand, a sample location is Longitude 174.7030220 and Latitude -36.8918260

Except at the equator, 1 unit of Longitude is <u>not</u> the same distance as 1 unit of Latitude. This makes using the data harder.
So often, the location data is converted to a simpler, local coordinate system called Northing / Easting. This conversion does not change the accuracy of the data.

Northing and Easting are both measured in meters, so 1 unit of Northing is the same distance as one unit of Easting. 

The origin of this measurement can be chosen at will. 
For each drone flight, SkyComb Analyst automatically chooses a nearby land point, that ensures that all drone locations are small positive numbers. 
For a specific drone flight, SkyComb Analyst converted the above Longitude/Latitude to Northing 26.30m, Easting 10.67m.

## Drone Location Accuracy
The primary data source for the location of the drone is GPS data.

Caveat: A drone may record a line of data in its flight log 30 times a second. 
The drone is <u>not</u> evaluating its GPS location 30 times a second. 
The drone is more likely to be evaluating its location once a second.

The secondary data source for the location of the drone is drone accelerometer data.
In the time between successive GPS evaluations, the drone generally uses the accelerometer data to update its location.

This real-time integration of GPS and accelerometer data is a source of location error in the flight log data.
This error shows up in the flight log as a series of steadily moving locations followed by a "jump" in location every say 30 frames, 
as new GPS data becomes available.

SkyComb Analyst automatically smooths the location data.


# Ground & Surface Elevation

## Ground & Surface Elevation Terminology
It is important to understand the difference between these two terms:

- Ground Elevation: The height of the ground above the sea level. 
- Surface Elevation: The height of the <u>tree tops</u> above the sea level. 

If the Ground Elevation is 170 meters, and the Surface Elevation is 177 meters, then the trees are 7 meters tall.
 
## Ground & Surface Elevation accuracy
Drones can <u>not</u> provide ground or surface elevation data. An alternative source of information is needed

Many countries have accurately mapped part or all of their land using a technology called 
[Lidar](https://en.wikipedia.org/wiki/Lidar/)
. Many countries provide this data to the public for free. 

For example, the New Zealand government is progressively mapping New Zealand. The resulting data is freely available at 
[LINZ](https://www.linz.govt.nz/products-services/data/types-linz-data/elevation-data).
The data is provided in 1 meter by 1 meter (horizontal) grids. The ground elevation (vertical) data accuracy is +/- 0.2 meters. That is +/- 20 centimeters which is amazing!
The surface elevation data has the same format and accuracy.

SkyComb Analyst can automatically integrate Lidar data for the area under a drone flight. 
Caveat: Currently only New Zealand Lidar data has been integrated so far.


# Drone Altitude vs Height

## Drone Altitude vs Height terminology 
Drones state their vertical distance above the ground using two different terms:
- Drone <u>Altitude</u>: The height of the drone above <u>Sea level</u>. Say 190 meters
- Drone <u>Height</u>: The height of the drone above the <u>Sea level</u> where it started its flight. Say 20 meters

For example, a drone placed on the ground in front of you, and switched on, will say it is at a height of 0.0 meters, but at an altitude of say 170 meters.

While drones can show their vertical distance above the ground using either Altitude or Height, the underlying data is the same.

## Drone Altitude & Height systemic error
Most drones calculate their Altitude/Height using 
[barometers](https://en.wikipedia.org/wiki/Barometer/)
. A barometer measures air pressure. Air gets thinner as the drone rises. 

So far so good. But barometeric pressure at sea level in one location can differ significantly from another sea level location. 
The same is true at in-land locations. 

For example, a drone sitting on the ground at sea level in New Zealand reported its altitude as 20 meters BELOW sea level!

Drones do <u>not</u> have a way to correct for this. 

If the operator uses the recommended flight protocols, 
SkyComb Analyst <u>has</u> can automatically correct this "systemic" error using Lidar ground elevation data.
This correction is accurate to within +/- 0.2m at the drone flight "start" and "end" points, 
but during the flight, as the drone is inherently an unstable flight platform, the height is much less accurately known.

## Drone Altitude & Height variable error
When say a storm front sweeps in, the air pressure changes. 
Barometers are effected by these air pressure changes, and the impact over the duration of a drone flight can be significant. 

For example, a drone that started and ended its flight in the SAME location in New Zealand, reported different altitudes at the start and end of the flight. 
The difference (error) was round 6 meters! There was no apparent change in the weather during this flight. So the cause of this error is not well understood.

Drones do <u>not</u> have a way to correct for this. 
If the operator uses the recommended flight protocols, 
SkyComb Analyst <u>has</u> an automated way to spread this variable error evenly over the flight duration.
This seems the best way to minimise the impact of this error on height data.

## Drone Altitude & Height overall error
Even with these enhancements, the drone height data is still the least accurate of all the drone data streams.

SkyComb Analyst has another automated way (described in a later section) to further refine the drone height data.



# Drone Logs

## Drone Log Interpretation
Drone flight logs are generally text files. The format depends on the drone model, but each new data set is stored on 1 to a few lines of text. 

Flight logs are updated in real-time. The drone periodically adds a new data set to the end of the text file - generally at the same rate as the video frame rate. 
So the log could be updated 30 times per second.

Various drone subsystems (e.g. GPS) refresh their data less frequently than that. 
So the data in each data set is the "last data collected" from each subsystem, and may not be accurate as at the frame timestamp.   

When a particular attribute <u>changes</u> assume that the related sub-system provided new data just before the frame timestamp

SkyComb Analyst understands this and compensates for it.
Caveat: SkyComb Analyst has only been extensively tested with a DJI M2E drone. 

## Drone Log Gaps
On rare occassions, the sub-system that updates the flight log may fail resulting in a gap (lack of data) in the flight log.

For example, a drone flight in New Zealand the flight log had a 1.5 second gap in the data. 
During this period, the drone continued to fly in the expected direction, at the expeected speed, but no log data was collected.

SkyComb Analyst automatically copes with these gaps.


# Optical and Thermal Videos
This section relates to drones that have both an optical and a thermal camera. 

## Video Resolution
The optical camera has a higher resolution than the thermal camera e.g. 1920x1080 vs 640x360. 

SkyComb Analyst automatically copes with this.

## Frame Rate
The optical camera has a higher frame rate than the thermal camera e.g. 30 frames/second vs 8 frames/second

SkyComb Analyst automatically copes with this.

## Field of Vision
The optical camera has a great field of vision than the thermal camera e.g. 85 degrees vs 57 degrees

SkyComb Analyst copes with this automatically for the DJI M2E drone by hard-coding ThermalVideo.HFOVDeg & OpticalVideo.HFOVDeg.
Caveat: For other drone models, other values may need to be hard-coded.

## Optical and Thermal Synchronisation - Part 1
The two cameras are distinct sub-systems, likely manufactured by different companies:
- The thermal video camera is simpler: It has a lower resolution, and saving the data in real-time is quick.
- The optical video camera is more complex: The resolution, colour palette, and frame frame are higher. The resulting image must be encoded (compressed) before storage. 

Both cameras must compress the data they see in real-time, but the above differences may result in the compressed data being persisted to the memory card at different rates.

These factors result in differences:
- The start date / time of the two video <u>files</u> may differ a little.
- The duration of the two videos may differ a little.
 
SkyComb Analyst copes with this automatically.

## Optical and Thermal Synchronisation - Part 2
The differences between the two cameras can result in the first frame of each video being captured at a slightly different time. 
That is, if you play the two videos side by side, one video will lag behind the other one. 

SkyComb Analyst provides a manual process for the operator to quickly determine the best "sychronization delay" for a given drone flight.
Refer to the [Flight](./Flight.md#optical-and-thermal-video-synchronisation) page for more detail.
After the operator enters the delay value in SkyComb Analyst, SkyComb Analyst stores the value 
in the FlightConfig.cs setting ThermalToOpticalVideoDelayS, and handles the sychronization automatically. 


# Gimbal 
The gimbal physically holds the camera(s) and compensates for small drone variable in yaw, pitch & roll, steadying the video image.

## Gimbal lag on turning
When the drone is flying in a straight line, and has to cope with say with changes in the cross-wind strength, this works well.

The gimbal is a distinct sub-system of the drone, and not perfectly co-ordinated with other drone sub-systems in real time.
When the drone starts to deliberately turn a corner, the gibmal may initially interpret the turn as a random variance to be "steadied".
So the drone may start turning say 0.5 seconds before the video starts turning. 
When the drone has completed its turn and is not pointing in the desired direction, the video may continue to turn, 
until the gimbal has caught up and is centered on the new direction.

While the flight log will contain the drone direction, information on the gimbal direction may not be contained in the flight log. 

SkyComb Analyst copes with this gimbal lag automatically.

## Camera down angle
The gimbal could be pointing the cameras at the horizon, or straight down at the ground, or somewhere inbetween.

This angle is key to SkyComb Analyst calculations. The drone flight log often does <u>not</u> contain this angle. 

SkyComb Analyst provides a manual process for the operator to specific the "camera down angle" for a given drone flight.
Refer [Flight](./Flight.md#camera-down-angle) page for more detail.
After the operator enters this value in SkyComb Analyst, SkyComb Analyst handles the calculations automatically. 

Caveat: The SkyComb flight protocol recommends the camera be pointed straight down during the flight. 
SkyComb Analyst has mostly been tested on flights with this camera configuration.


# Thermal Video Processing Errors
The above sections detail errors that can be quickly analysed when loading the drone flight data and associated Lidar data. 
That is, the above corrections are implemented without relying on the contents of the videos.

This section details errors related to the processing of the thermal video.

## Thermal Video Resolution
The SkyComb Analyst image processing algorithms are limited by the resolution and frame rate of the thermal video. 
While the thermal video may have a resolution of 640x360, the underlying sensor may have a lower resolution, 
with some on-camera hardware algorithm generated the higher-resolution video.

## Thermal Threshold
Thermal image processing algorithms must look at an image and decide which pixels are "hot" 
and which are "not hot" using a "threshold value". 

SkyComb Analyst can't automatically detect or calculate the "best" threshold value.
SkyComb Analyst provides a way for the operator to determine the best value.
Once the operator has entered this value, SkyComb Analyst applies the threshold automatically.

## Drone Height & Object Location
The "Comb" image processing algorithm detects objects - on the ground or in trees above ground.

Frame by frame, using the estimated drone height, SkyComb Analyst calculates the Northing / Easting location of the object.
Each frame is an independent experiment.
If the estimated drone height is correct, then the location of the object in each frame cluster at one physical location.
If the estimated drone height is <u>incorrect</u>, then the location of the object in each frame appear as a line walking across the land, aligned to the drone direction-of-flight.
If several independent objects are being tracked in the same video image, all these objects move in the same pattern.

SkyComb Analyst "back calculates" an improved drone height that would minimise the movement of all the visible objects in a flight leg. 
It applies this improved drone height to the full flight leg.

In test flights, where 8 hot objects were concurrently visible in the same image of a thermal video, 
this method improved the drone height by 3.2 meters, and improved the location object clustering significantly to be +/- 8 cms!

There is good reason to believe that this approach is correctly calculating the drone height.

These improved drone height per flight leg  are "pushed back" into the drone data for future use.

## Object Height
The "Comb" image processing algorithm takes the same objects detected above, and determines whether they are on the ground or in trees above ground.

It does this using the [Parallax](https://en.wikipedia.org/wiki/Parallax) method. 
As the drone moves overhead, the angle from the drone to the object changes.

The more frames the object is in view, the greater the drone "base line" movement distabce, the greater the change in angle from drone to object, 
and the more accurate the object height calculation.

The main constraint on the accuracy of this method is the accuracy of the "drone to object angle". 
This is calculated from the drone location (good accuracy), the location of the object in the thermal video image.
As the thermal video image has low resolution, the "drone to object angle" accuracy is not great.
