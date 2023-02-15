# [SkyComb Analyst - Models](https://github.com/PhilipQuirke/SkyCombAnalystHelp/) 

# Overview
This ReadMe covers the image processing techniques embedded in the SkyComb Analyst application.
(Refer the root-level [ReadMe](./README.md) for an overview of the whole application.)


# Purpose
This tool supports several image processing models that can be applied to videos. 

The models output markedly different images. 
Example model outputs are shown [here](./Static/ModelExamples.png).


# Simple Models
A few "simple" models process each video frame independently. No data is persisted between frames:

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


# Complex Models
There are two "complex" models. These models process each frame of the video, but also persist data between frames to derive additional information. The models are called:
- Flow
- Comb 

## Flow Model
Aka Optical Flow. Aka OpticalFlowPyrLK. 
Uses the Gftt process output as input, this process tracks significant visual things across mutiple frames drawing their visual progress over time as a "worm". 
Uses settings FlowWindowSize, FlowMaxPyramid, FlowMinEigThreshold, DrawFlowHotPixels.  
This algorithm also uses the Smooth and Threshold processes.

## Comb Model
Specific to this application, the Comb model is the "recommended" model for thermal videos. 

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

The altitude reported by the drone is often inaccurate. The inaccuracy causes the calculated physical location of the object in each successive frame to move a regular distance in the direction of flight, giving a straight line of object locations. The Comb process can back-calculate from this line, to correct the drone altitude, and correct the object line to be an object point. In this example, 8 test hot spots appear to all be moving in the same direction. After correcting the drone altitude, the 8 test hot spots are correctly identified as stationary:

![FixAltitudeM](./Static/FixAltitudeM.png?raw=true "Fix Altitude Example")


# Source Code
The source code folder ModelSpace the implementation of these models.


# Drone Specifics 
Each manufacturer's drones needs unique configuration settings

## Mavic 2 Enterprise Dual 
For a Mavic 2 Enterprise (M2E) Dual drone with the thermal camera "Gain Mode" set to "High (-10C to 140C)":
- Thresholding works well with ThresholdProcess=Binary and ThresholdValue=230. The Comb process uses the same ThresholdValue.

## Autel Evo 2 640T
For a Autel Evo 2 640T:
- Thresholding works well with ThresholdProcess=Binary and ThresholdValue=150. The Comb process uses the same ThresholdValue.
