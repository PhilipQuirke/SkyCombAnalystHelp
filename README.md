# [SkyComb Analyst Help](https://github.com/PhilipQuirke/SkyCombAnalystHelp/) 

# Introduction
SkyComb Analyst processes data collected by drones equipped with thermal and optical video cameras. It detects animals & shows their size, temperature & height above ground. It generates (thermal & optical) close up videos of the animals.

![Object Explorer](./Static/ObjectExplorer.png?raw=true "Object Explorer")

Drones are unstable flying platforms. The data they generate contains many inaccuracies. If you follow the SkyComb Analyst recommendations on how to fly your drone, SkyComb Analyst can automatically compensate for several inaccuracies. 

![Path, Speed & Altitude](./Static/Overview1.png?raw=true "Path, Speed & Altitude")

Where it is available, SkyComb Analyst supplements the drone data with very accurate ground and tree top **elevation** data from public sources, increasing the accuracy of **animal height** estimates.

![DEM & DSM Elevations](./Static/Overview2.png?raw=true "DEM & DSM Elevations")

SkyComb Analyst can generate animal population statistics for the area flown over, in a robust and repeatable fashion. It generates [spreadsheets](./DataStore.md) and annotated video as output. This output can used later for further analysis e.g. as input to image recognition machine learning systems.

SkyComb Analyst provides an easy to use [interface](./UserInterface.md) that makes it easy to explore the data your drone collected.

![User Interface](./Static/UIExample.png?raw=true "User Interface")


# Index
These pages provide more detail:
- The [Flight](./Flight.md) page explains how to fly your drone missions to collect high-quality data.
- The [UserInterface](./UserInterface.md) page explains how to use the SkyComb Analyst tool to analyse your drone flight data. 
- The [Drone](./Drone.md) page explains aspects of the drone and drone-related source code.
- The [DataStore](./DataStore.md) page explains the spreadsheet used by the application to store data.
- The [Errors](./Errors.md) page describes all known error sources & how they are minimised. 
- The [Ground](./Ground.md) page explains how detailed ground and treetop elevation data is obtained and displayed.
- The [Process](./Process.md) page explains the image processing options the application supports.


# Source Code
The source code is written in C# and stored in [SkyComb Analyst Code](https://github.com/PhilipQuirke/SkyCombAnalyst/). 
The main source files are:
- CommonSpace folder: Shared utility classes
- DrawSpace folder: Classes to annotate videos and to draw graphs in the UI
- PersistModel folder: Refer [DataStore](./DataStore.md)
- DroneModel folder: Refer [Drone](./Drone.md)
- DroneLogic folder: Refer [Drone](./Drone.md)
- GroundSpace folder: Refer [Ground](./Ground.md)
- ProcessModel folder: Refer [Process](./Process.md) 
- ProcessLogic folder: Refer [Process](./Process.md) 
- RunSpace folder: Classes to run a process model over an image or video(s)
- UserInterface folder: Forms used by the application including MainForm.cs the main UI page


# Tooling 
Developed using:
- Emgu, a C# wrapper around the OpenCV image processing library. Refer nuget package in project
- EPPlus, a spreadsheet tool. Refer nuget package in project
- Visual Studio Community 2022 downloaded from https://visualstudio.microsoft.com/vs/community/

# Caveats
This application has only been extensively tested with:
- Data from a DJI Mavic 2 Enterprise (M2E) Dual drone. SkyComb Analyst is designed to support any drone, but other drone models may require some code changes around flight log parsing and loading. Refer [Drone](./Drone.md) for more details.
- Data generated using the [Flight](./Flight.md) page data collection recommendations, especially: 1) the flight starts and ends on the ground and 2) the camera(s) are pointing straight down during the flight. SkyComb Analyst will support other flight configurations, but the height accuracy will be worse.  
- Ground (surface and treetop) data for New Zealand. SkyComb Analyst is designed to support any country, but supporting additional countries will involve locating publically available ground data, and parsing and loading that data. Refer [Ground](./Ground.md) for more detail.
