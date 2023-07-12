# [SkyComb Analyst](https://github.com/PhilipQuirke/SkyCombAnalystHelp/blob/main/README.md) User Interface


## Overview
The SkyComb Analyst tool helps environmentalists, conservationists & scientists use a thermal drone as a scientific tool.
The primary use case is a drone with thermal and optical camera, flying over wilderness, detecting animals. 

This page assumes you have already:
- Collected video & flight log data by flying a drone mission as recommended in the [Flight](./Flight.md) page. 
- Copied the video & flight log data from the drone to your computer as described in [DroneDataPort](./DroneDataPort.md) page. 
This page details how to use SkyComb Analyst to analyse the video.


## Step 0: Run SkyComb Analyst
Run the SkyComb Analyst tool. 


## Step 1: Selecting a Video
Click the "Select Video" button and choose one of your thermal or optical video files:
- The flight log for the thermal video will be processed. This can take a few seconds. 
- Detailed ground and surface elevation data for the area under the drone flight path will be obtained. This can take a few seconds.  
- Several graphs will be displayed
- SkyComb will find the "Legs" (long straight sections) in the flight, and display corresponding buttons labelled "A", "B", etc. 
- SkyComb will default the "From/To (Secs)" fields matching the first and last legs found.
- Images from the thermal and optical videos at the "From Secs" position will be displayed.

![Main form](./Static/UIExamplePostLoad.png?raw=true "Main form")

At the same time, a spreadsheet containing the above data, graphs etc will be automatically created on disk. 
This spreadsheet is called the [DataStore](./DataStore.md)
The spreadsheet name is based on the thermal video file name but with the suffix "_SkyComb.xlsx"


## Step 2: Drone Settings
Click the "Drone Settings" button to edit settings related to the drone and its flight:

![Drone Settings](./Static/DroneSettings.png?raw=true "Drone Settings")

These settings are detailed in the [DroneSettings](./DroneSettings.md) page. 


## Step 3: Process Settings
Click the "Process Settings" button to edit settings related to image processing:

![Process Settings](./Static/ProcessSettings.png?raw=true "Process Settings")

These settings are detailed in the [ProcessSettings](./ProcessSettings.md) page. 


### Selecting Legs
You may not want to process all the legs that SkyComb Analyst has detected. 
For example, the first leg may be the drone moving to the start of the search grid. 
If you want to de-select Leg "A", then ctrl-click on the Leg "A" button. 
This will change the "From (Secs)" field. 
 
Likewise, the last leg may be the drone moving back to the launch point.  
This will change the "To (Secs)" field. 

You can select the set of legs to process by clicking (select), ctrl-clicking (deselect), and shift-clicking (add) on the Leg buttons.
You must select a contiguous range of legs like "B" to "N" - you can't deselect a leg to give a hole in the middle of the range.  


## Step 4: Start Run
- Click the "All" Legs button (or select the range of Legs you want to process).
- Set the "Process" to "Comb". 
- Set the "Speed" to "Fast" or "Max". 
- Click "Save"
- Click "Start Run"


### Progress Indicators
While the video image process is being run:
- The video frame(s) currently being processed, annotated with any objects found, are shown. Note: If the Speed is set to "Max" speed then the UI is only updated every 100 frames. This is the fastest processing mode.
- Various graphs in are updated to show the position of the drone and any objects found.
- A sequence of progress messages progress at bottom left of the page.
| Message    | Description |
| ---------- | ----------- |
| Loading    | The video meta-data is loaded and the entire flight data files (if any) are loaded & Drone Speed, Altitude and Path graphs are displayed |
| Processing | Frame by frame loading, processing & displaying of the video(s) |
| Saving     | The video and spreadsheet (if any) are saved |
| Finished   | Shows total elapsed time (including loading, processing, UI updating and saving). |


## The output
When the image processing run has finished, the object list appears:

![Main form](./Static/UIExample.png?raw=true "Main form")

Also, these files are automatically saved on disk:
- The annotated thermal video is saved to a file named InputFileName_SkyComb.mp4
- Much thermal & optical meta-data, drone flight path and altitude data, ground and tree-top elevation, objects detected data is saved to the [DataStore](./DataStore.md)


### Viewing all objects found
In the main page, the objects are shown on the Flight Path graph in orange and red. 
Clicking on the "pop-out" button above the Flight Path graph gives this expanded view:

![DroneFlightPathForm](./Static/DroneFlightPathForm.png?raw=true "Drone Flight Path Form")

Summary statistics about the object population are shown on the left.

Using the "Show" radio buttons, you can change background on the flight path to show either the surface (aka tree-top, in shades of green), the ground (in shades of brown), or the area imaged by the drones thermal video camera.   


### Viewing individual objects found
In the main page, the list shows all the objects found.
Clicking on the "pop-out" button at top-left of this list opens the Object Explorer form:

![Object Explorer](./Static/ObjectExplorer.png?raw=true "Object Explorer")

This page allows you to select and focus in on any single object & review much of the data associated with that object.

Each object has been detected over several video frames. Each frame generated a "Feature" associated with the object. 
The object features are shown in the list at bottom right.

This page "loops" through the object features, so you can see the order the data was collected in. 
You can click the "Pause" button to stop or start this looping.


## Later Viewing
If you close down SkyComb Analyst, and come back later, and select the same video, the flight and object information is quickly loaded from the DataStore, and shown.
That is, you can review the flight and object data without reruning the image processing step.
