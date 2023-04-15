# [SkyComb Analyst Help - DataStore](https://github.com/PhilipQuirke/SkyCombAnalystHelp/) 

# Overview
The [SkyComb Analyst](https://github.com/PhilipQuirke/SkyCombAnalyst/) tool 
generates a lot of data and graphs about the drone flight, videos and object found. 
This data is persisted in a spreadsheet called a DataStore. 
This page describes the DataStore and its uses. 
(Refer the root-level [ReadMe](./README.md) for an overview of the whole tool.)


# Purpose
The [SkyComb Analyst](https://github.com/PhilipQuirke/SkyCombAnalyst/) tool generates a lot of data. 

To help users view and post-analyze the data, the data is persisted (stored) in a spreadsheet (called a DataStore).
The spreadsheet is very human-readable and includes graphs.

The DataStore acts as a _database_ for a drone flight.
A user may run the same video several times with different settings. Each run takes time. 
To speed up runs, the DataStore is used to cache information for re-use in successive runs.

The DataStore is named InputFileName_SkyComb.xlsx and is created in the location specified in the setting "OutputDirectory". 

A sample datastore is [here](./Static/DJI_0094_SkyComb.xlsx)

# Controlling output files
Two user interface controls impact how much data the tool saves: 
- SaveAnnotatedVideo: Determines whether an output video file is created. Value is "Yes" or "no". 
- SaveObjectData: Determines whether Object and Featurestabs area is created in the DataStore. Value is "All", "Significant" or "None". 

# DataStore Structure
The DataStore has 3 main parts:
- **Files**: A single tab lsting the input files read, and the output files created
- **Drone**: The "Drone" tab and the following 7 tabs. The data in these tabs is calculated when the user selects the video. This data exists (and is saved to the DataStore) before any video image processing is run.
- **Process**:  The "Process" tab and the following 5 or 6 tabs. This data only exists _after_ the video image processing is run.

# DataStore Tabs
The DataStore contain some or all of these tabs:
- **Files**: Lists the input files read, and the output files created
- **Drone**: Summarises the drone video metadata, drone flight path meta-data, ground elevations, surface elevations and other settings related to:
	- **Sections**: Lists the raw flight sections data detailing the drone flight. 
	- **Sections2**: Holds graphs based on the raw drone Sections data, including:
		- The flight path in the Northing / Easting coordinate system
		- The flight path in the original Longitude / Latitude coordinate system   	
		- The lineal distance travelled (in meters) by the drone per section, graphed over time 
		- The lineal speed (in meters / second) of the drone per section, graphed over time
		- The change of direction (aka delta yaw, in degrees / section) of the drone, graphed over time 
		- The change of pitch (aka nose up / down, in degrees / section) of the drone, graphed over time 
		- The change of roll (in degrees / section) of the drone, graphed over time 
	- **Ground**: Lists the ground elevation (DEM) data. Includes a 3D graph of the ground elevations.
	- **Surface**: Lists the surface (aka tree-top) elevation (DSM) data. Includes a 3D graph of the surface elevations.
	- **Legs**: Lists "legs" of flight path - at constant altitude, in constant direction of a reasonable duration over a reasonable distance. 
	- **Steps**: List flight data derived from flight steps using smoothing/correction algorithms, ground data, etc.
	- **Steps2**: Holds graphs based on the smoothed Steps data, including:
		- The flight path in the Northing / Easting coordinate system
		- The altitude of the drone, the ground elevation and surface (aka tree-top) elevation (in meters) graphed over time	
		- The lineal distance travelled (in meters) by the drone per step, graphed over time 
		- The lineal speed (in meters / second) of the drone per step, graphed over time
		- The change of direction (aka delta yaw, in degrees / step) of the drone, graphed over time 
		- The change of pitch (aka nose up / down, in degrees / step) of the drone, graphed over time 
		- The change of roll (in degrees / step) of the drone, graphed over time 
		- The duration of the flight legs, graphed over time 
- **Process**: Summarises the process settings, run settings, run results, etc related to the following tabs:
	- **Blocks**: Lists the Blocks corresponding to the processed video frames
	- **Blocks2**: Holds graphs based on the Blocks data, for the processed video frames, including:
		- The altitude of the drone, the ground elevation and surface (aka tree-top) elevation (in meters) graphed over time	
		- The lineal distance travelled (in meters) by the drone per step, graphed over time 
		- The lineal speed (in meters / second) of the drone per step, graphed over time
		- The change of direction (aka delta yaw, in degrees / step) of the drone, graphed over time 
		- The change of pitch (aka nose up / down, in degrees / step) of the drone, graphed over time 
		- The change of roll (in degrees / step) of the drone, graphed over time 
		- The duration of the flight legs, graphed over time 
	- **Pixels**: Lists the hot Pixels found. (Normally not saved as it is too bulky)
	- **Features**: Lists the Features found during block processing. A Feature is a dense clusters of hot Pixels in a Block
	- **Objects**: Lists the Objects found during block processing. For the Comb process, an Object is a series of Features that physically overlap in several frames 
	- **Objects2**: Holds graphs based on the Objects & Features data, including:
		- Apparent speed of the features and objects found, graphed over time   
		- Estimated height of the features and objects found, graphed over time   
		- The location of the features & objects found (in Northing / Easting meter units)
		- The location of the features & objects found (in Northing / Easting meter units) with drone steps overlaid
	

# DataStore caches configuration settings
When a video is run, the tool saves all configuration settings to the spreadsheet. 
This includes all settings visible in the UI and also those not visible in the UI.

When the user selects a video, the tool looks for an existing InputFileName_SkyComb.xlsx 
in the OutputDirectory. If one is found:
- The settings visible in the UI are loaded from the spreadsheet.
- The existing Ground elevation data is re-used
- The existing drone flight path, altitude, etc data is re-used
- Significant objects found in the last run are reloaded and displayed


# Creating / Updating the DataStores 
A new spreadsheet is created in three parts:
- When a video is selected, by clicking the 'Select File' button, the Files tab is populated and the spreadsheet is created.
- Immediately, some initial calculations are done, much drone-specific data is calculated, several "drone" tabs created, and the spreadsheet updated.
- If the user clicks the "Save" button (generally after changing some UI settings), the above data related to the drone flight is re-saved.
- If the user clicks the "Run" button, much image processing data is calculated, several "model" tabs are created, and the spreadsheet updated.

After each step the spreadsheet is saved and closed, so you can view it in Excel. 
Remember to close it again before running the new step in SkyComb Analyst.
