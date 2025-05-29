# [SkyComb Analyst](https://github.com/PhilipQuirke/SkyCombAnalystHelp/blob/main/README.md) - DataStore

## Overview
The SkyComb Analyst tool generates a lot of data and graphs about the drone flight, videos and object found. 
This data is persisted in a spreadsheet called a DataStore. This page describes the DataStore and its uses. 
(Refer the root-level [ReadMe](./README.md) for an overview of the whole tool.)


## Purpose
The SkyComb Analyst tool generates a lot of data. 
To help users view and post-analyze the data, the data is persisted (stored) in a spreadsheet (called a DataStore).
The spreadsheet is very human-readable and includes graphs.

A DataStore acts as a _database_ for a drone flight.
A user may run the same video several times with different settings. Each run takes time. 
To speed up runs, the DataStore is used to cache information for re-use in successive runs.

The DataStore is named [InputFileName]_SkyComb.xlsx and is created in the location specified in the setting "OutputDirectory". 

A sample datastore is [here](./Static/DJI_20240416142614_0001_T_SkyComb.xlsx)

## DataStore Structure
The DataStore has 5 main parts:
- **Home tab**: A single tab listing and linking to the various tabs
- **Animals, Drone and Ground tabs**: These are the three report tabs, giving overview tables and graphics
- **Settings tabs**: These include file settings (input files read, and the output files created), "Drone settings", and "Process settings" tabs. The latter two list the settings selected by the user in the run, and give key summary data from the run.
- **Data tabs**: These contain the detailed reports from the analysis. The three tabs are giving data about flight legs, identfied animals, and distinct features.
- **Hidden data tabs**:  These contain other detailed input and output data, that are less useful for users, but may be viewed if desired.

## User Interface controls
All the fields in the user interface editable by the user are persisted to the DataStore. 

Two editable fields also impact the volume of data the tool persists: 
- SaveAnnotatedVideo: Determines whether an output video file is created. Value is "Yes" or "no". 
- SaveObjectData: Determines whether Object and Features tabs area is created in the DataStore. Value is "All", "Significant" or "None". 

If later the user re-loads the same video, the tool looks for an existing InputFileName_SkyComb.xlsx. If it finds one:
- The user-editable settings are loaded from the spreadsheet into the user interface.
- The existing drone flight path, ground elevation data, surface elevation data, etc is loaded and re-used
- The graphs etc are updated with the loaded data 

## DataStore Tabs
The DataStore contain some or all of these tabs, as well as others:
- **Home**: Lists the spreadsheet tabs, their purpose, and links to them
- **Animals**: An overview report on animals found, including a size histogram and a flight path display with animal locations at particular elevations. Note that eleveation data is only meaningful from drone video rather than drone stills.
- **AnimalsData**: Lists each identified animal, together with its characteristics. These include source (frame, or seconds seen for  a video), location (northing and easting, together with error), distance from drone ("Lineal M"), height (only valid with drone video), size, ground height, the number of hot pixels on the image assigned to that animal, the size of the box around those pixels, the size of the oval forming the animal body (girth, spine in pixels and cms).
- **FileSettings**: Lists the input files read, and the output files created
- **DroneSettings**: Summarises the drone video metadata, drone flight path meta-data, ground elevations, surface elevations and other settings related to:
	- **Sects1**: Lists the raw flight sections data detailing the drone flight. 
	- **Sects2**: Holds graphs based on the raw drone Sections data, including:
		- The flight path in the Northing / Easting coordinate system
		- The flight path in the original Longitude / Latitude coordinate system   	
		- The lineal distance travelled (in meters) by the drone per section, graphed over time 
		- The lineal speed (in meters / second) of the drone per section, graphed over time
		- The change of direction (aka delta yaw, in degrees / section) of the drone, graphed over time 
		- The change of pitch (aka nose up / down, in degrees / section) of the drone, graphed over time 
		- The change of roll (in degrees / section) of the drone, graphed over time 
	- **DEM**: Lists the ground elevation (aka DEM) data. Includes a 3D graph of the ground elevations.
	- **DSM**: Lists the surface (aka tree-top) elevation (aka DSM) data. Includes a 3D graph of the surface elevations.
	- **Legs**: Lists "legs" of flight path - at constant altitude, in constant direction of a reasonable duration over a reasonable distance. 
	- **Steps1**: List flight data derived from flight steps using smoothing/correction algorithms, ground data, etc.
	- **Steps2**: Holds graphs based on the smoothed Steps data, including:
		- The flight path in the Northing / Easting coordinate system
		- The altitude of the drone, the ground elevation and surface (aka tree-top) elevation (in meters) graphed over time	
		- The lineal distance travelled (in meters) by the drone per step, graphed over time 
		- The lineal speed (in meters / second) of the drone per step, graphed over time
		- The change of direction (aka delta yaw, in degrees / step) of the drone, graphed over time 
		- The change of pitch (aka nose up / down, in degrees / step) of the drone, graphed over time 
		- The change of roll (in degrees / step) of the drone, graphed over time 
		- The duration of the flight legs, graphed over time 
- **ProcessSettings**: Summarises the process settings, run settings, run results, etc related to the following tabs:
	- **Blks1**: Lists the Blocks corresponding to the processed video frames
	- **Blks2**: Holds graphs based on the Blocks data, for the processed video frames, including:
		- The altitude of the drone, the ground elevation and surface (aka tree-top) elevation (in meters) graphed over time	
		- The lineal distance travelled (in meters) by the drone per step, graphed over time 
		- The lineal speed (in meters / second) of the drone per step, graphed over time
		- The change of direction (aka delta yaw, in degrees / step) of the drone, graphed over time 
		- The change of pitch (aka nose up / down, in degrees / step) of the drone, graphed over time 
		- The change of roll (in degrees / step) of the drone, graphed over time 
		- The duration of the flight legs, graphed over time 
	- **Pxls**: Lists the hot Pixels found. (Normally not saved as it is too bulky)
	- **Feats**: Lists the Features found during block processing. A Feature is a dense clusters of hot Pixels in a Block
	- **Objs1**: Lists the Objects found during block processing. For the Comb process, an Object is a series of Features that physically overlap in several frames 
	- **Objs2**: Holds graphs based on the Objects & Features data, including:
		- Apparent speed of the features and objects found, graphed over time   
		- Estimated height of the features and objects found, graphed over time   
		- The location of the features & objects found (in Northing / Easting meter units)
		- The location of the features & objects found (in Northing / Easting meter units) with drone steps overlaid
	- **Legs2**: For each flight path Leg, show the object movement calculations used to refine the drone's altitude in that leg.
	- **Popln**: Object population summary statisitcs
	

## Creating / Updating the DataStores 
A new spreadsheet is created in three parts:
- When a video is selected, by clicking the 'Select File' button, the Files tab is populated and the spreadsheet is created.
- Immediately, some initial calculations are done, much drone-specific data is calculated, several tabs are created, and the spreadsheet updated.
- If the user clicks the "Save" button (generally after changing some UI settings), the above data related to the drone flight is re-saved.
- If the user clicks the "Run" button, much image processing data is calculated, several "model" tabs are created, and the spreadsheet updated.

After each step the spreadsheet is saved and closed, so you can view it in Excel. 
Remember to close it again before running the new step in SkyComb Analyst.
