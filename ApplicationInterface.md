# [SkyComb Analyst - Application Interface](https://github.com/PhilipQuirke/SkyCombAnalyst/) 


# Overview
SkyComb Analyst helps environmentalists, scientists & software developers make a drone into a scientific tool.
The primary use case is a drone with thermal and optical camera, flying over wilderness, detecting animals. 

This document assumes you have already collected data by flying a drone mission as explained in [End to End Usage](./Usage.md)

This document details more about the application user interface and how to use it.


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

