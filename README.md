# [SkyComb Analyst](https://github.com/PhilipQuirke/SkyCombAnalystHelp/) 

# Background
SkyComb Analyst is a tool aimed at environmentalists, scientists & software developers. 
It allows drones equipped with thermal and optical video cameras, to fly over forests, 
to detect animals, in a repeatable fashion, giving a robust statistical estimate of the animal population. 
It converts thermal drones from toys into scientific data-collection platforms. 


# What does it do?
SkyComb Analyst decodes the "flight log" data capturing by the drone during the flight. 
It displays flight path, speed, altitude, yaw, etc data:  

![Path, Speed & Altitude](./Static/Overview1.png?raw=true "Path, Speed & Altitude")

It decodes the drone flight area, and loads highly-detailed (1m grid) and 
highly-accurate publically-available ground-elevation data (+/- 0.2m) and 
tree-top height data for the area the drone flew over. It stores this data:

![DEM & DSM Elevations](./Static/Overview2.png?raw=true "DEM & DSM Elevations")

It combines the drone, ground and tree-top altitude data. If you follow our recommended flight protocols, 
SkyComb Analyst can automatically correct for drone elevation inaccuracies (which are common):

![Drone Altitude Correction](./Static/OnGroundAtExamples.png?raw=true "Drone Altitude Correction")

It automatically finds the sections of the flight that have a (mostly) constant altitude, in a (mostly) constant direction 
for a reasonable length of time. These it calls "legs". For each leg, it processes the drone thermal video, 
detecting animals, and displaying the results:

![Thermal & Optical Videos](./Static/Overview3.png?raw=true "Thermal & Optical Videos")

The overall user interface of this Windows based tool looks like this:

![User Interface](./Static/UIExample.png?raw=true "User Interface")

The raw and derived data and the visualisations can be saved on disk as a video and/or as a spreadsheet (for further analysis).



# Usage

## Input files
Supported drone input is 1) two videos and two flight logs (recommended), 2) a video and flight log or 3) a video file 

After the program starts up, the input video(s) can be chosen and loaded via the "Select video" button.
Alternatively a input video name can be specified in the App.Config setting "InputFileName".
This will be automatically loaded on start up.

[DroneReadMe](./DroneReadMe.md) provides more detail on the input videos, 
their contents and accuracy, obtaining ground elevation data, and how to view all this metadata. 
Also recommended config settings for specific drone types.

[Usage](./Usage.md) provides more detail on flying drone data collection missions.  

## Run Configuration
The image-processing model applied to the input video is controlled by many configuration settings. 
The most important App.Config settings are:
| Setting  | Description |
| -------- | ----------- |
| RunModel | Determines which image processing model to use to process the input. Value is "Contour", "Distance, "Flow", "Gftt", "Comb", "Smooth", "Threshold" or "None".  |
| RunVideoFromS | Determines the time (in seconds) to start video input processing from. Optional |
| RunVideoToS | Determines the time (in seconds) to end video input processing at. Optional |

After the program starts up, these settings can be modified in the UI, allowing different combinations to be tested.

## Run Execution
If the "RunModel" and "InputFileName" settings are defaulted in App.Config, 
then the program will run the specified processing technique on the default input on start up.

After the program starts up, the "Run" button can be used to manually run/re-run the processing technique.
If the RunSpeed setting is set to "Max" the UI is updated infrequently during processing (to save time).
Otherwise, during processing the UI images and graphs will be updated often.
Either way these runtime messages are shown:
| Message    | Description |
| ---------- | ----------- |
| Loading    | The video meta-data is loaded and the entire flight data files (if any) are loaded & Drone Speed, Altitude and Path graphs are displayed |
| Processing | Frame by frame loading and processing of the video |
| Saving     | The video, image and spreadsheets (if any) are saved |
| Finished   | Shows total elapsed time (including loading, processing, UI updating and saving). |
| Objects    | Number of objects and significant objects detected is shown |

Once the processing has finished, the updated image, video and spreadsheet files are written to disk. 
The progress message is updated at each step, finally saving "Loaded in 8s. Ran in 6s (1036 frames). 
Saved in 9s. Finished after total of 30s. Objects 1 (1 significant)".

[Usage](./Usage.md) provides more detail on processing data gathered in drone data collection missions.  

## Saving output files
The program output is:
- Displaying the image or video frame currently being processed, and the updated image or video frame in the UI.
- Saving the updated image or video to a file named InputFileName_SkyComb.mp4(or jpg)
- Saving thermal & optical meta-data, drone flight path and altitude data, ground and tree-top elevation to a spreadsheet file named InputFileName_SkyComb.xls

[DataStoreReadMe](./DataStoreReadMe.md) file provides more detail on the spreadsheet contents, purpose and usage.

# Image Processing Models
The user can select one of several image processing models via the RunModel dropdown. 
This can help users understand/experiment with these models.

The available models are None, Smooth, Threshold, Flow, Comb (recommended), Contour, Distance and Gftt.
The models output markedly different images. 

![Model Examples](./Static/ModelExamples.png?raw=true "Model Examples")

[ModelReadMe](./ModelReadMe.md) file provides more detail on the models. 
Also recommended config settings for specific drone types.


# Source Code
The source code is written in C#. The main source files are:
- App.Config: Default value for all input, process, and output configuration settings.
- CommonSpace folder: Shared utility classes
- DataStoreSpace folder: Refer [DataStoreReadMe](./DataStoreReadMe.md)
- DrawSpace folder: Classes to draw on videos and on the UI
- DroneSpace folder: Refer [DroneReadMe](./DroneReadMe.md)
- GroundSpace folder: Refer [GroundReadMe](./GroundReadMe.md)
- ModelSpace folder: Refer [ModelReadMe](./ModelReadMe.md) 
- RunSpace folder: Classes to run a process model over an image or video(s)
- Mainform.cs: The only UI page of this application


# Tooling 
Developed using:
- Emgu, a C# wrapper around the OpenCV image processing library. Refer nuget package in project
- EPPlus, a spreadsheet tool. Refer nuget package in project
- Visual Studio Community 2022 downloaded from https://visualstudio.microsoft.com/vs/community/
