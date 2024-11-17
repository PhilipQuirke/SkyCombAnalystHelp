# [SkyComb Analyst](https://github.com/PhilipQuirke/SkyCombAnalystHelp/blob/main/README.md) User Interface

## Overview
The SkyComb Analyst tool helps environmentalists, conservationists & scientists use a thermal drone as a scientific tool.
The primary use case is a drone with thermal camera, flying over wilderness, detecting animals. 

This page assumes you have already:
- Collected video & flight log data by flying a drone mission as recommended in the [Flight](./Flight.md) page. 
- Copied the video & flight log data from the drone to your computer as described in [DroneDataPort](./DroneDataPort.md) page. 
This page details how to use SkyComb Analyst to analyse the video.

## Step 0: Run SkyComb Analyst
Run the SkyComb Analyst tool. 

## Step 1: Selecting a Video
Click the "Open" button and choose one of your thermal video files:
- The flight log for the thermal video will be processed. This can take a few seconds. 
- Detailed ground and surface elevation data for the area under the drone flight path will be obtained. This can take a few seconds.  
- Several graphs will be displayed
- SkyComb will find the "Legs" (long straight sections) in the flight, and display corresponding buttons labelled "A", "B", etc. 
- SkyComb will default the "From/To (Secs)" fields matching the first and last legs found.
- An image from the video at the "From Secs" position will be displayed.

![Main form](./Static/UIExamplePostLoad.png?raw=true "Main form")

At the same time, a spreadsheet containing the above data, graphs etc will be automatically created on disk. 
This spreadsheet is called the [DataStore](./DataStore.md)
The spreadsheet name is based on the thermal video file name but with the suffix "_SkyComb.xlsx"

## Step 2: Process the video
Click the "Run" button at left.

Optionally, click the "Drone Settings" button to edit settings related to the drone and its flight. Refer [DroneSettings](./DroneSettings.md) for more detail. 

Optionally, click the "Process Settings" button to edit settings related to image processing. Refer [ProcessSettings](./ProcessSettings.md) for more detail. 

Click "Start Run". On a fast laptop, a 30 minute video can take 10 minutes to prcoess.
While the video image process is being run:
- The video frame(s) currently being processed, annotated with any objects found, are shown.
- Various graphs in are updated to show the position of the drone and any objects found.

When the image processing run has finished, the object list appears at bottom right:

![Main form](./Static/UIExample.png?raw=true "Main form")

## Step 3: Drone Path Explorer
In the main page, the objects are shown on the Flight Path graph in orange and red. 
Clicking on the "pop-out" button above the Flight Path graph gives this expanded view:

![DroneFlightPathForm](./Static/DroneFlightPathForm.png?raw=true "Drone Flight Path Form")

## Step 4: Object Explorer
In the main page, the list at bottom right shows the objects found.
Clicking on the "pop-out" button at top-left of this list opens the Object Explorer form:

![Object Explorer](./Static/ObjectExplorer.png?raw=true "Object Explorer")

Refer [ObjectExplorer](./ObjectExplorer.md) for more detail.

## Later Viewing
If you close down SkyComb Analyst, and come back later, and select the same video, the flight and object information is quickly loaded from the DataStore, and shown.
That is, you can review the flight and object data without reruning the image processing step.
