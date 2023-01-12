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
tree-top height data for the area the drone flew over:

![DEM & DSM Elevations](./Static/Overview2.png?raw=true "DEM & DSM Elevations")

It combines the drone, ground and tree-top altitude data. If you follow our recommended flight protocols, 
SkyComb Analyst can automatically correct for (very common) drone altitude inaccuracies:

![Drone Altitude Correction](./Static/OnGroundAtExamples.png?raw=true "Drone Altitude Correction")

It automatically finds the parts of the drone flight that have a (mostly) constant altitude, in a (mostly) constant direction 
for a reasonable length of time. These it calls "legs". For each leg, it processes the drone thermal video, 
detecting animals, and displaying the results:

![Thermal & Optical Videos](./Static/Overview3.png?raw=true "Thermal & Optical Videos")

The overall user interface of this Windows based tool looks like this:

![User Interface](./Static/UIExample.png?raw=true "User Interface")

The raw and derived data and the visualisations are saved on disk as a video and/or as a spreadsheet (for further analysis and re-use).



# Usage

## Select Video
For a given drone flight, SkyCombAnalyst can process 1) two videos and two flight logs (recommended), 2) a video and flight log or 3) a video file 

After the program starts up, an input video can be chosen via the "Select video" button.

[Drone](./Drone.md) provides more detail on the input videos, 
their contents and accuracy, obtaining ground elevation data, and how to view this metadata. 

[Usage](./Usage.md) provides more detail on flying drone data collection missions.  

## Run Configuration
The image-processing model applied to the input video is controlled by many configuration settings. 
The most important settings are:
| Setting  | Description |
| -------- | ----------- |
| RunModel | Determines which image processing model to use to process the input. Value is "Contour", "Distance, "Flow", "Gftt", "Comb", "Smooth", "Threshold" or "None".  |
| RunVideoFromS | Determines the time (in seconds) to start video input processing from. Optional |
| RunVideoToS | Determines the time (in seconds) to end video input processing at. Optional |

These settings can be modified in the UI, allowing different combinations to be tested.

## Run Processing
After the video is selected & loaded, the "Run" button will run/re-run the image processing technique.
If the RunSpeed setting is set to "Max" the UI is updated infrequently during processing (to save time).
Otherwise, the UI images and graphs will be updated often.
Either way these runtime messages are shown:
| Message    | Description |
| ---------- | ----------- |
| Loading    | The video meta-data is loaded and the entire flight data files (if any) are loaded & Drone Speed, Altitude and Path graphs are displayed |
| Processing | Frame by frame loading and processing of the video |
| Saving     | The video and spreadsheets (if any) are saved |
| Finished   | Shows total elapsed time (including loading, processing, UI updating and saving). |
| Objects    | Number of objects and significant objects detected is shown |

Once the processing has finished, the updated video and spreadsheet files are written to disk. 
The progress message is updated at each step, finally saving "Loaded in 8s. Ran in 6s (1036 frames). 
Saved in 9s. Finished after total of 30s. Objects 1 (1 significant)".

[Usage](./Usage.md) provides more detail on processing data gathered in drone data collection missions.  

## Saving output files
The program output is:
- Displaying the video frame currently being processed, and the updated video frame in the UI.
- Saving the updated video to a file named InputFileName_SkyComb.mp4
- Saving thermal & optical meta-data, drone flight path and altitude data, ground and tree-top elevation to a spreadsheet file named InputFileName_SkyComb.xls

[DataStore](./DataStore.md) file provides more detail on the spreadsheet contents, purpose and usage.

# Image Processing Models
The user can select one of several image processing models via the RunModel dropdown. 
This can help users understand/experiment with these models.

The available models are None, Smooth, Threshold, Flow, Comb (recommended), Contour, Distance and Gftt.
The models output markedly different images. 

![Model Examples](./Static/ModelExamples.png?raw=true "Model Examples")

[Model](./Model.md) file provides more detail on the models. 
Also recommended config settings for specific drone types.


# Source Code
The source code is written in C#. The main source files are:
- CommonSpace folder: Shared utility classes
- DataStoreSpace folder: Refer [DataStore](./DataStore.md)
- DrawSpace folder: Classes to draw on videos and on the UI
- DroneSpace folder: Refer [Drone](./Drone.md)
- Forms folder: Forms used by the application including MainForm.cs the main UI page
- GroundSpace folder: Refer [Ground](./Ground.md)
- ModelSpace folder: Refer [Model](./Model.md) 
- RunSpace folder: Classes to run a process model over an image or video(s)


# Tooling 
Developed using:
- Emgu, a C# wrapper around the OpenCV image processing library. Refer nuget package in project
- EPPlus, a spreadsheet tool. Refer nuget package in project
- Visual Studio Community 2022 downloaded from https://visualstudio.microsoft.com/vs/community/
