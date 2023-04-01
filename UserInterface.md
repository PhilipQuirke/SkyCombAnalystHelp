# [SkyComb Analyst - User Interface](https://github.com/PhilipQuirke/SkyCombAnalyst/) 


# Overview
SkyComb Analyst helps environmentalists, scientists & software developers make a drone into a scientific tool.
The primary use case is a drone with thermal and optical camera, flying over wilderness, detecting animals. 

This page assumes you have already collected data by flying a drone mission as explained in the [Usage](./Usage.md) page

This page details more about the application user interface and how to use it.


# Input Settings

## Selecting a Video
Run the SkyComb Analyst tool. 

Click "Select" and choose one of your thermal or optical video files:
- The flight log for the thermal video will be processed. This can take a few seconds. 
- Detailed ground and surface elevation data for the area under the drone flight path will be obtained 
- Several graphs will be displayed
- SkyComb will find the "Legs" (long straight sections) in the flight, and display corresponding buttons labelled "A", "B", etc. 
- SkyComb will default the "From/To (Secs)" fields matching the first and last legs found.
- Images from the thermal and optical videos at the "From Secs" position will be displayed.

![UI Sample](./Static/UIExample.png?raw=true "UI Example")

At the same time, a spreadsheet containing the above data, graphs etc will be automatically created on disk. 
The spreadsheet name will reflect the thermal video file name but with the suffix "_SkyComb.xlsx"
This spreadsheet acts like a database or datastore.


## Optical to Thermal Video Delay
Differences between the thermal and optical cameras can result in the first frame of each video being captured at a slightly different time. 
In one example, there was a difference of 0.5 seconds between the first frame of each video.
SkyComb Analyst needs the videos to be time synchronised.

To evaluate this setting for your drone video:
1. Set the "Video delay (secs)" to "0"
2. Click "Run" and watch both the thermal and optical videos are the same time. 
3. As the drone turns a corner, see if the thermal and optical video images start to "turn" at the same time. If they do, they are sychronized.
4. If the images do not turn at the same time, increase or decrease "Video delay (secs)".
5. Repeat Step 2 etc until the videos sync up.

Click "Save" to save all settings to the spreadsheet.


## Camera Down Angle
On a drone, the camera gimbal controls where camera is pointing. 
SkyComb Analyst needs to know this value, and this value is <u>not</u> available from the drone flight log.

If the camera was pointing:
- straight down during the flight, then set "Camera down angle" to 90 (not -90) in the SkyComb Analyst UI.
- straight forward (horizontally), then set "Camera down angle" to 0.
- half way between straight down and straight forward, then set "Camera down angle" to 45.  

Click "Save" to save all settings to the spreadsheet.


## On Ground At 
SkyComb Analyst can more accurately calculate the height of the drone if the drone was on the ground at the start and/or end of the flight/video.
This information is <u>not</u> available from the drone flight log.

Use the "On ground at" field to inform SkyComb Analyst when the drone was on the ground. Select one of the settings:
- <b>Start</b> : The drone was on the ground at the start of the video (only). 
- <b>End</b> : The drone was on the ground at the end of the video (only). 
- <b>Both</b> : The drone was on the ground at both the start and end of the video. (This is the recommended approach & gives the best results).
- <b>Auto</b> : Use this if you don't know the answer

The user interface includes a "Drone Altitude" chart that shows the ground elevation in brown, the tree-top height in green and drone altitude in blue.
Inaccurate elevations as measured by the drone can be corrected if the "On ground at" setting is specified.

This diagram shows the inaccurate drone altitudes for an example flight that started and ended on the ground.
The altitude graph this  flight are shown four times, demonstrating how the different "On ground at" settings is used mitigate the inaccuracies. 

![On Ground At Examples](./Static/OnGroundAtExamples.png?raw=true "On Ground At Examples")

Click "Save" to save all settings to the spreadsheet.


# Image Processing Settings

## Process
The [Process](./Process.md) page describes the supported image processing algorithms. 
Leave the value set to the recommended default value "Comb".

## Threshold value
Thermal image processing algorithms must look at an image and decide which pixels are "hot" 
and which are "not hot" using a "threshold value". 

SkyComb Analyst can't automatically detect or calculate the "best" ThresholdValue.
You must calculate the best threshold value: 
- Too low a value and SkyComb Analyst will detect lots of "false hit" objects.
- Too high a value and SkyComb Analyst will not detect any objects.

To calculate the best threshold value:
1. Set the "Run speed" to "Fast".
2. Set the "Threshold value" to "235".
3. Click "Run" & watch the thermal video, until you see a hot object detected that looks interesting. Note the time it appears.
4. Halt the run by clicking "Stop"
5. Set "From/To (Secs)" to a few seconds before the object was detected, to a few seconds after it was detected. 
6. Try increasing the "Threshold value" to say "240". Click "Run" and watch the object. Was the object outline better defined?
7. Try decreasing the "Threshold value" to say "230". Click "Run" and watch the object. Was the object outline better defined?
8. Repeat this process until you are happy with the Threshold Value

Threshold Values as low as 150 and as high as 235 have been seen with various drone thermal videos.



# Process the whole video
Having configued the above parameters which are specific to your drone and flight, you are ready to process the video.

Set the "Process" to "Comb". Clear the "From (Secs)" and "To (Secs)" settings. Click "Run"





# Application Interface

## Run Configuration
The image-processing model applied to the input video is controlled by many configuration settings. 
The most important settings are:
| Setting  | Description |
| -------- | ----------- |
| RunVideoFromS | Determines the time (in seconds) to start video input processing from. Optional |
| RunVideoToS | Determines the time (in seconds) to end video input processing at. Optional |
| RunProcess | Determines which image processing model to use to process the input. Value is "Contour", "Distance, "Flow", "Gftt", "Comb", "Smooth", "Threshold" or "None".  |

These settings can be modified in the UI, allowing different combinations to be tested.

## Run Processing
After the video is selected & loaded, the "Run" button will run/re-run the image processing technique.
If the RunSpeed setting is set to "Max" the UI is updated infrequently during processing (to save time).
Otherwise, the UI images and graphs will be updated often.
Either way these runtime messages are shown:
| Message    | Description |
| ---------- | ----------- |
| Loading    | The video meta-data is loaded and the entire flight data files (if any) are loaded & Drone Speed, Altitude and Path graphs are displayed |
| Processing | Frame by frame loading, processing & displaying of the video(s) |
| Saving     | The video and spreadsheet (if any) are saved |
| Finished   | Shows total elapsed time (including loading, processing, UI updating and saving). |
| Objects    | Number of objects and significant objects detected is shown |

Once the processing has finished, the updated video and spreadsheet files are written to disk. 
The progress message is updated at each step, finally saving "Loaded in 8s. Ran in 6s (1036 frames). 
Saved in 9s. Finished after total of 30s. Objects 1 (1 significant)".

The [Usage](./Usage.md) page provides more detail on processing data gathered in drone data collection missions.  

## Saving output files
The program output is:
- Displaying the video frame currently being processed, and the updated video frame in the UI.
- Saving the updated video to a file named InputFileName_SkyComb.mp4
- Saving thermal & optical meta-data, drone flight path and altitude data, ground and tree-top elevation, objects detected to a spreadsheet file named InputFileName_SkyComb.xls

The [DataStore](./DataStore.md) page has more detail on the spreadsheet contents, purpose and usage.
