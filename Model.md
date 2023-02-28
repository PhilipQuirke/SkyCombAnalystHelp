# [SkyComb Analyst - Processes](https://github.com/PhilipQuirke/SkyCombAnalystHelp/) 

# Overview
This ReadMe covers the image processing techniques embedded in the SkyComb Analyst application.
(Refer the root-level [ReadMe](./README.md) for an overview of the whole application.)


# Purpose
This tool supports several image processing models that can be applied to videos. 

The processes output markedly different images. 
Example process outputs are shown [here](./Static/ModelExamples.png).


# Simple Processes
A few "simple" proceses transform each video frame independently. No data is persisted between frames:

- None: No changes to the input image are made. The output mirrors the input. Useful for debugging & measuring processing "overhead".
- Smooth: Smooths or average each pixel value in each frame. Useful on "staticy" input. The "SmoothPixels"" setting determines the area over which each pixel is smoothed. The "SmoothProcess" setting sets the algorithm to one of:
	- Blur 
	- Gaussian
	- Median (default)
	- None
- Threshold: Converts all pixels below (or above) a specified threshold (ThresholdValue) to black in each frame. Useful to highlight hot objects in a thermal image. The "ThresholdProcess" setting sets the algorithm to one of:
	- Binary (default)
	- BinaryInv
	- ToZero 
	- ToZeroInv
	- Trunc
	- None
- Contour: Finds objects by colour change across their boundary edge in each image. Use setting ContourMinArea to only select objects containing at least this many pixels.
- Distance: Hard to describe. Refer OpenCV DistanceTransform doco. Have not found useful. Uses settings DistanceMinGray and DistanceMaskSize 
- Gftt: The "Good feature to track" process finds significant visual things that might be worth tracking over time e.g. the corner of a car. This algorithm use the associated settings GfttMaxCorners, GfttQualityLevel, GfttMinDistance, GfttBlockSize, GfttUseHarris and GfttK. This algorithm also uses the Smooth and Threshold processes.


# Complex Processes
There are two "complex"processing models. These processes transform each frame of the video, but also persist data between frames to derive additional information. The processes are called:
- Flow
- Comb 

## Flow Process
Aka Optical Flow. Aka OpticalFlowPyrLK. 
Uses the Gftt process output as input, this process tracks significant visual things across mutiple frames drawing their visual progress over time as a "worm". 
Uses settings FlowWindowSize, FlowMaxPyramid, FlowMinEigThreshold, DrawFlowHotPixels.  
This algorithm also uses the Smooth and Threshold processes.

## Comb Process
Specific to this application, the Comb process is the "recommended" process for thermal videos. 

This model processes the video by:
- removing noise from the image (using "Median" Smoothing)
- detecting "hot" pixels in each grayscale frame (using "Binary" Thresholding)
- finding "Features" which are dense clusters of hot pixels in each frame (using CombFeature.PixelNeighborSearch) 
- finding "Objects" which are Features that persist across several frames (say >1 second) in the same area, taking into account movements in camera's point of view (using CombObject.ClaimFeature).

This model processes drone data by:
- Using drone flight log data (e.g. longitude, latitude, altitude) 
- Deriving ground speed from the flight data.

The Comb process decides whether an object is significant using a number of factors:
- Count: The object must have enough hot pixels to be significant. Up to a certain limit, bigger objects are more significant.
- Density: The object's hot pixels must be constrained to a small area.
- Time: The object must be visible across several frames (i.e. time duration) 
- Elevation: Hot objects above ground level are more significant. This corresponds to the hot object moving at a different speed to the ground (because of parallex).

For significant objects, the UI shows "Notes" such as "Yes: C3 D2 T1 E3" showing the strength of each factor.  

The altitude reported by the drone is often inaccurate. The inaccuracy causes the calculated physical location of the object in each successive frame to move a regular distance in the direction of flight, giving a straight line of object locations. The Comb process automatically back-calculates from these lines, to correct the drone altitude, and correct the object lines to be closer to object points. In this real-world example, 8 test hot spots appear to all be moving in the same direction. After correcting the drone altitude, the 8 test hot spots are correctly shown as stationary:

![FixAltitudeM](./Static/FixAltitudeM.png?raw=true "Fix Altitude Example")

The altitude correction algorithm code is in ProcessCombLeg.cs, and the results of the algorthim are stored in the "CombLeg" tab of the DataStore. 


# Source Code
The source code folders ProcessModel and ProcessLogic contain the implementation of these models.


# Drone Specifics 
Each manufacturer's drones needs unique configuration settings

## Mavic 2 Enterprise Dual 
For a Mavic 2 Enterprise (M2E) Dual drone with the thermal camera "Gain Mode" set to "High (-10C to 140C)":
- Thresholding works well with ThresholdProcess=Binary and ThresholdValue=230. The Comb process uses the same ThresholdValue.

## Autel Evo 2 640T
For a Autel Evo 2 640T:
- Thresholding works well with ThresholdProcess=Binary and ThresholdValue=150. The Comb process uses the same ThresholdValue.
