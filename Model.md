# [SkyComb Analyst - Models](https://github.com/PhilipQuirke/SkyCombAnalystHelp/) 

# Overview
This ReadMe covers the purpose and content of the ModelSpace folder of the SkyComb Analyst application.
(Refer the root-level [ReadMe](./README.md) for an overview of the whole application.)


# Purpose
This tool supports several processing models that can be applied to images and videos. 
The ModelSpace folder contains the implementation of these models.

The models output markedly different images. 
Example model outputs are shown [here](./Static/ModelExamples.png).


# Simple Models
These "simple" models process each video frame independently. 
No data is persisted between frames:

- None: No changes to the input image are made. The output mirrors the input. Useful for debugging & measuring processing "overhead".
- Smooth: Smooths or average each pixel value in each frame. Useful on "staticy" input. The "SmoothPixels"" setting determines the area over which each pixel is smoothed. The "SmoothProcess" setting sets the algorithm to one of:
	- Blur 
	- Gaussian
	- Median (recommended)
	- None
- Threshold: Converts all pixels below (or above) a specified threshold (ThresholdValue) to black in each frame. Useful to highlight hot objects in a thermal image. The "ThresholdProcess" setting sets the algorithm toone of:
	- Binary (recommended)
	- BinaryInv
	- ToZero 
	- ToZeroInv
	- Trunc
	- None
- Contour: Finds objects by colour change across their boundary edge in each image. Use setting ContourMinArea to only select objects containing at least this many pixels.
- Distance: Hard to describe. Refer OpenCV DistanceTransform doco. Have not found useful. Uses settings DistanceMinGray and DistanceMaskSize 
- Gftt: The "Good feature to track" process finds significant visual things that might be worth tracking over time e.g. the corner of a car trunk. Use settings GfttMaxCorners, GfttQualityLevel, GfttMinDistance, GfttBlockSize, GfttUseHarris and GfttK. Uses the Smooth and Threshold processes.


# Complex Models
Two "complex" models only work on videos (not images). These models process each frame of the video, but also persist data between frames to derive additional information:
- Flow
- Comb 

## Flow Model
Aka Optical Flow. Aka OpticalFlowPyrLK. 
Uses the Gftt process output as input, this process tracks significant visual things across mutiple frames drawing their visual progress as a "worm". 
Uses settings FlowWindowSize, FlowMaxPyramid, FlowMinEigThreshold, DrawFlowHotPixels. Uses the Gftt and Smooth models.

## Comb Model
Specific to this application, the Comb model is the "recommended" model for thermal videos. 

This model processes the video by:
- removing noise from the image (using "Median" Smoothing)
- detecting "hot" pixels in each grayscale frame (using "Binary" Thresholding)
- finding "Features" which are dense clusters of hot pixels in each frame (using CombFeature.PixelNeighborSearch) 
- finding "Objects" which are Features that persist across several frames (i.e. time duration) in the same area, taking into account movements in camera's point of view (using CombObject.ClaimFeature).

This model processes drone data by:
- Using drone flight log data (e.g. longitude, latitude, altitude) associated with the video, but in a separate file.
- Deriving ground speed from the flight data.

This model also uses a "child" Flow process to further refine ground & object speed estimates.

The Comb process decides whether an object is significant using a number of factors:
- Count: The object must have enough hot pixels to be significant. Up to a certain limit, bigger objects are more significant.
- Density: The object's hot pixels must be constrained to a small area.
- Time: The object must be visible across several frames (i.e. time duration) 
- Elevation: Hot objects above ground level are more significant. This corresponds to the hot object moving at a different speed to the ground (because of parallex).

For significant objects, the UI shows "Notes" such as "Yes: C3 D2 T1 E3" showing the strength of each factor.  


# Source Code
The significant source files in the ModelSpace folder are:
- Model.cs: The in-memory data models of significant pixels, features derived from collections of these pixels for most models.
- ModelFlow.cs: Expanding on Model.cs, contains the in-memory data models specific to the Optical Flow process, including objects derived from sequences of features.
- ModelComb.cs: Expanding on Model.cs, contains the in-memory data models specific to Comb process, including objects derived from sequences of features.
- ModelConfig.cs: Contains configuration settings e.g. SmoothProcess, SmoothPixels, ThresholdProcess, ThresholdValue
- ModelFactory.cs: Generates model objects.


# Drone Specifics 
Each manufacturer's drones needs unique configuration settings

## Mavic 2 Enterprise Dual 
For a Mavic 2 Enterprise (M2E) Dual drone with the thermal camera "Gain Mode" set to "High (-10C to 140C)":
- Thresholding works well with ThresholdProcess=Binary and ThresholdValue=230. The Comb process uses the same ThresholdValue.

## Autel Evo 2 640T
For a Autel Evo 2 640T:
- Thresholding works well with ThresholdProcess=Binary and ThresholdValue=150. The Comb process uses the same ThresholdValue.

