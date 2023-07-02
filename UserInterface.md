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

The Save button is only enabled after changes are made by the user, and it shows the number of changes. Click "Save" to save all the settings to the [DataStore](./DataStore.md)


### Use Video From / To 
These settings show the portion of the video that will be processed by SkyComb Analyst. 

The default settings are from the start of the first Leg to the end of the last Leg.


### On Ground At 
SkyComb Analyst can more accurately calculate the height of the drone if the drone was on the ground at the start and/or end of the flight/video.
This information is <u>not</u> available from the drone flight log.

Use the "On ground at" field to inform SkyComb Analyst when the drone was on the ground. Select one of the settings:
- **Start** : The drone was on the ground at the start of the video (only). 
- **End** : The drone was on the ground at the end of the video (only). 
- **Both** : The drone was on the ground at both the start and end of the video. (This is the recommended approach & gives the best results).
- **Auto** : Use this if you don't know the answer

The user interface includes a "Drone Altitude" chart that shows the ground elevation in brown, the tree-top height in green and drone altitude in blue.
Inaccurate elevations as measured by the drone can be corrected if the "On ground at" setting is specified.

This diagram shows the inaccurate drone altitudes for an example flight that started and ended on the ground.
The altitude graph this  flight are shown four times, demonstrating how the different "On ground at" settings is used mitigate the inaccuracies. 

![On Ground At Examples](./Static/OnGroundAtExamples.png?raw=true "On Ground At Examples")


### Camera Down Angle
On a drone, the camera gimbal controls where camera is pointing. 
SkyComb Analyst needs to know this value, and this value is **not** available from the drone flight log.

If the camera was pointing:
- straight down during the flight, then set "Camera down angle" to 90 (not -90) in the SkyComb Analyst UI.
- straight forward (horizontally), then set "Camera down angle" to 0.
- half way between straight down and straight forward, then set "Camera down angle" to 45.  


### Optical to Thermal Video Delay
For some drone flights, the first frame of the thermal and optical videos may start at slightly different times (e.g. 0.3 seconds different) 
and the optical and thermal videos will be slightly out of sync.  
SkyComb Analyst needs the videos to be time synchronised.

The "Video delay (secs)" setting handles this difference and synchronises the videos. To tune this setting for your drone video:
1. Set the "Video delay (secs)" setting to 0 & click Save
2. Click "Process Settings", set the "Speed" setting to Fast & click Save
3. Click "Run" and watch both the thermal and optical videos at the same time. 
4. As the drone turns a corner, see if the thermal and optical video images start to "turn" at the same time. If they do, they are sychronized, and there is nothing more to do!
5. If the images do *not* turn the corner at the same time:
    - Click Stop
    - Increase or decrease "Video delay (secs)" by say +/= 0.1 seconds
    - Repeat Steps 3 & 4 until the videos sync up.


## Step 3: Process Settings
Click the "Process Settings" button to edit settings related to image processing:

![Process Settings](./Static/ProcessSettings.png?raw=true "Process Settings")

The Save button is only enabled after changes are made by the user, and it shows the number of changes. Click "Save" to save all the settings to the [DataStore](./DataStore.md)


### Processing Algorithm
The [Process](./Process.md) page describes the supported image processing algorithms. 
Leave the value set to the default value "Comb".


### Gray Scale "Hot" Threshold
Thermal image processing algorithms must look at an image and decide which pixels are "hot" 
and which are "not hot" using a "threshold value" in the range 0 to 255. 

SkyComb Analyst can't automatically detect or calculate the "best" ThresholdValue.
You must calculate the best threshold value: 
- Too low a value and SkyComb Analyst will detect lots of "false hit" objects.
- Too high a value and SkyComb Analyst will not detect any objects.

Threshold Values as low as 150 and as high as 235 have been seen with various drone thermal videos.

To calculate the best threshold value for your video:
- Set the "Run speed" to "Fast". 
- Set the "Threshold value" to "235".
- Click "Run" & watch the thermal video, until you see a hot object detected that looks interesting. Note the time it appears.
- Halt the run by clicking "Stop"
- Set "From/To (Secs)" to a few seconds before the object was detected, to a few seconds after it was detected. 
- Try increasing the "Threshold value" to say "240". Click "Run" and watch the object. Was the object outline better defined?
- Try decreasing the "Threshold value" to say "230". Click "Run" and watch the object. Was the object outline better defined?
- Repeat this process until you are happy with the Threshold Value


### Selecting Legs
You may not want to process all the legs that SkyComb Analyst has detected. 
For example, the first leg may be the drone moving to the start of the search grid. 
If you want to de-select Leg "A", then ctrl-click on the Leg "A" button. 
This will change the "From (Secs)" field. 
 
Likewise, the last leg may be the drone moving back to the launch point.  
This will change the "To (Secs)" field. 

You can select the set of legs to process by clicking (select), ctrl-clicking (deselect), and shift-clicking (add) on the Leg buttons.
You must select a contiguous range of legs like "B" to "N" - you can't deselect a leg to give a hole in the middle of the range.  

Click "Save" to save all settings to the [DataStore](./DataStore.md)


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
