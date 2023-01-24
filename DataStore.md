# [SkyComb Analyst - DataStore](https://github.com/PhilipQuirke/SkyCombAnalystHelp/) 

# Overview
The SkyComb Analyst application generates a lot of data and graphs about the videos and logs of a drone flight. 
This data is persisted in a spreadsheet (called a DataStore) which acts as a database for a drone flight.
This ReadMe describes the DataStore and its uses. 
(Refer the root-level [ReadMe](./README.md) for an overview of the whole application.)


# Purpose
The SkyComb Analyst application supports several processing models that can be applied to videos. 
These models generate much data. To help users view and post-analyze the data, the data is stored in a spreadsheet 
named InputFileName_SkyComb.xlsx. The spreadsheet is very human-readable and includes graphs.

A user may run the same video several times with different settings. Each run takes time. 
To speed up runs, the spreadsheet is used as a database to cache data for re-use in successive runs.
For example, the spreadsheet "Ground" tab acts like a database table of cached ground elevations. 

The DataStore contains several graphs including a 3D rendering of the ground elevation data:

![DataStore Example Ground Graph](./Static/Overview2.png?raw=true "DataStore Example Ground Graph")


# Controlling output files
The tool output is controlled by these settings, which can be edited in the UI:
- SaveImageFile: Determines whether an output video file is created. Value is "True" or "False". 
- SaveObjects: Determines whether a spreadsheet tab containing Object data is created. Value is "All", "Some" or "None". 
- SaveFeatures: Determines whether a spreadsheet tab containing Feature data is created. Value is "All", "Some" or "None". 

The output is created in the location specified in the setting "OutputDirectory". 
If this is not specified, the output is created in the same directory the input video is in.
		

# DataStore caches configuration settings
When a video is run, the tool saves all configuration settings to the spreadsheet. 
This includes all settings visible in the UI and also those not visible in the UI.

When the user selects a video, the tool looks for an existing InputFileName_SkyComb.xlsx 
in the OutputDirectory. If one is found:
- The settings visible in the UI are loaded from the spreadsheet.
- The existing Ground elevation data is re-used
- The existing drone flight path, altitude, etc data is re-used
- Significant objects found in the last run are reloaded and displayed


# DataStore Content
The spreadsheet (aka DataStore) named InputFileName_SkyComb.xlsx can contain these tabs:
- Files: Lists the input file(s) read, and the output file(s) created
- Drone: Summarises the drone video(s) meta-data, drone flight path meta-data, ground elevations, and other settings.
- Sections: Lists the raw flight sections data detailing the drone flight. 
- Sections2: Holds graphs based on the raw drone Sections data, including:
	- The flight path in the Northing / Easting coordinate system
	- The flight path in the original Longitude / Latitude coordinate system   	
	- The lineal distance travelled (in meters) by the drone per section, graphed over time 
	- The lineal speed (in meters / second) of the drone per section, graphed over time
	- The change of direction (aka delta yaw, in degrees / section) of the drone, graphed over time 
	- The change of pitch (aka nose up / down, in degrees / section) of the drone, graphed over time 
	- The change of roll (in degrees / section) of the drone, graphed over time 
- Ground: Lists the ground elevation (DEM) data. Includes a 3D graph of the ground elevations.
- Surface: Lists the surface (aka tree-top) elevation (DSM) data. Includes a 3D graph of the surface elevations.
- Legs: Lists "legs" of flight path - at constant altitude, in constant direction of a reasonable duration over a reasonable distance. 
- Steps: List flight data derived from flight steps using smoothing/correction algorithms, ground data, etc.
- Steps2: Holds graphs based on the smoothed Steps data, including:
	- The flight path in the Northing / Easting coordinate system
	- The altitude of the drone, the ground elevation and surface (aka tree-top) elevation (in meters) graphed over time	
	- The lineal distance travelled (in meters) by the drone per step, graphed over time 
	- The lineal speed (in meters / second) of the drone per step, graphed over time
	- The change of direction (aka delta yaw, in degrees / step) of the drone, graphed over time 
	- The change of pitch (aka nose up / down, in degrees / step) of the drone, graphed over time 
	- The change of roll (in degrees / step) of the drone, graphed over time 
	- The duration of the flight legs, graphed over time 
- Model: Summarises the processing model settings, run settings, run results, etc.
- Blocks: Lists the Blocks corresponding to the processed video frames
- Blocks2: Holds graphs based on the Blocks data, including:
-  
- Pixels: Lists the hot Pixels found. (Often skipped as it is too bulky)
- Features: Lists the Features found. A Feature is a dense clusters of hot Pixels in a Block
- Objects: Lists the Objects found. For the COmb process, an Object is a series of Features that overlap in several successive frames 
- Objects2: Holds graphs based on the Objects & Features data. 


# Creating / Updating the DataStores 
A new spreadsheet is creation in three steps:
- When a video is selected, by clicking the 'Select File' button, the Files tab is populated and the spreadsheet is created.
- Immediately, some initial calculations are done, much drone-specific data is calculated, several tabs created, and the spreadsheet updated.
- If the user clicks the "Save" button (generally after changing some UI settings), the above data related to the drone flight is re-saved.
- If the user clicks the "Run" button, much image processing data is calculated, several tabs created, and the spreadsheet updated.

After each step the spreadsheet is saved and closed, so you can view it in Excel. 
Remember to close it again before running the new step in SkyComb Analyst.
