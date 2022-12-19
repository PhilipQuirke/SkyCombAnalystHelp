# [SkyComb Analyst - DataStore](https://github.com/PhilipQuirke/SkyCombAnalyst/) 

# Overview
This ReadMe covers the purpose and content of the DataStoreSpace folder of the SkyComb Analyst application.
(Refer the root-level [ReadMe](./ReadMe.md) for an overview of the whole application.)


# Purpose
This tool supports several processing models that can be applied to images and videos. 
These models generate much data. To help users view and post-analyze the data, the data is stored in a spreadsheet 
named InputFileName_SkyComb.xlsx. The spreadsheet is very human-readable and includes graphs.

A user may run the same video several times with different settings. Each run takes time. 
To speed up runs, the spreadsheet is used as a "DataStore" to cache data for re-use in successive runs.
For example, the spreadsheet "Ground" tab acts like a database table of cached ground and tree-top elevations. 

The DataStore contains several graphs including a 3D rendering of the ground elevation data:
![DataStore Example Graphs](../Static/XlsExampleGraphs.png?raw=true "DataStore Example Graphs")


# Controlling output files
The tool output is controlled by these settings, which can be edited in the UI:
- SaveImageFile: Determines whether image / video file is created. Value is "True" or "False". 
- SaveObjects: Determines whether a spreadsheet tab containing Object data is created. Value is "All", "Some" or "None". 
- SaveFeatures: Determines whether a spreadsheet tab containing Feature data is created. Value is "All", "Some" or "None". 

The output is created in the location specified in the setting "OutputDirectory". 
If this is not specified, the output is created in the same directory the input video is in.
		

# DataStore caches configuration settings
When a video is run, the tool saves all configuration settings to the spreadsheet. 
This includes all settings visible in the UI and also those not visible in the UI.

Some of the UI configuation settings (e.g. Camera down angle) can be different for each video. 
For this reason, when the user selects a video, the tool looks for an existing InputFileName_SkyComb.xlsx 
in the OutputDirectory. If one is found:
- The settings visible in the UI are loaded from the spreadsheet.
- The existing Ground elevation data is re-used
- The existing drone flight path, altitude, etc data is re-used
- Notes on any significant objects found in the last run are reloaded


# DataStore Content
The spreadsheet (aka DataStore) named InputFileName_SkyComb.xlsx can contain these tabs:
- Files: Lists the input file(s) read, and the output file(s) created
- Drone: Summarises the drone video(s) meta-data, drone flight path meta-data, ground elevations, and other settings.
- Sections: Lists the flight sections (aka steps) detailing the drone flight path. 
- Ground: Lists the ground elevation (DEM) data. Includes a 3D graph of the ground elevations.
- Surface: Lists the surface (aka tree-top) elevation (DSM) data. Includes a 3D graph of the surface elevations.
- Steps: List flight data derived from flight steps using algorithms & ground data.  
- Legs: Lists "legs" of flight path - at constant altitude, in constant direction of a reasonable duration over a reasonable distance. 
- Charts: Graphical charts of the previous (drone and ground related) tabs
- Model: Summarises the processing model settings, run settings, run results, etc.
- Blocks: Lists the Blocks corresponding to the processed video frames. Includes a graph of the ground and frame speed.
- Pixels: Lists the hot Pixels found. (Often skipped as it is too bulky)
- Features: Lists the Features found. A Feature is a dense clusters of hot Pixels in a Block
- Objects: Lists the Objects found. An Object is a series of Features that overlap in several successive frames 
- Flow: Graphical charts related to the "flow" process output (also populated when using the "comb" process)
- Comb: Graphical charts related to the "comb" process output


# Creating / Updating the DataStores 
A new spreadsheet is creation in three steps:
- When a video is selected, by clicking the 'Select File' button, the Files tab is populated and the spreadsheet is created.
- Some initial calculations are done and the Files, Drone, Sections, Ground, Steps, Legs are calculated for the entire drone flight, corresponding tabs created, and the spreadsheet is updated.
- When a process model is run over the video, by clicking the 'Run' button, the Run, Blocks, Pixel, Feature, Object, Flow and Comb data is calculated, the corresponding tabs created, and the spreadsheet is updated.

After each step the spreadsheet is saved and closed, so you can view it in Excel. 
Remember to close it again before running the new step in SkyComb Analyst.
