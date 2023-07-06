# SkyComb Analyst Help

## Purpose
The SkyComb Analyst tool helps environmentalists, conservationists & scientists use a thermal drone as a scientific tool 
to collect information on wild animal populations in an automated, robust, repeatable, cost-effective & safe way.

## Video Introduction
This 4 minute introductory video overviews the tool https://www.youtube.com/watch?v=QY1EAinyYJM

## Description
The SkyComb Analyst tool processes data collected by drones equipped with thermal and optical video cameras. It detects animals:

![FlightPathForm](./Static/DroneFlightPathForm.png?raw=true "Flight Path Form")

For each animal detected it shows their size, temperature & height above ground. 
It generates (thermal & optical) close up videos of each animal.
You can category the animals and exclude objects you are not interested in.

![Object Explorer](./Static/ObjectExplorer.png?raw=true "Object Explorer")

Drones are complex tools that move in three dimensions. The data they generate contains many inaccuracies. If you follow the SkyComb Analyst [recommendations](./Flight.md) on how to fly your drone, SkyComb Analyst can automatically compensate for [several inaccuracies](./Errors.md)

Where it is available, SkyComb Analyst supplements the drone data with very accurate ground and tree top **elevation** data from public (Lidar) sources, increasing the accuracy of **animal height above ground** estimates.

![DEM & DSM Elevations](./Static/Overview2.png?raw=true "DEM & DSM Elevations")

SkyComb Analyst automatically finds animals in the area flown over, in a robust and repeatable fashion. You can easily view each animal found. The tool generates [spreadsheets](./DataStore.md) and annotated video as output. This output supports further offline analysis e.g. as input to image recognition machine learning systems.

SkyComb Analyst provides an easy to use [interface](./UserInterface.md) that makes it quick to explore the data your drone collected.

![User Interface](./Static/UIExample.png?raw=true "User Interface")


## Index of Content
These pages provide more detail on the tool and its use:
- The [Flight](./Flight.md) page explains how to fly your drone missions to collect high-quality data.
- The [UserInterface](./UserInterface.md) page explains how to use the SkyComb Analyst tool to analyse your drone flight data. 
- The [Drone](./Drone.md) page explains drone terminology related to the SkyComb Analyst tool.
- The [DroneDataPort](./DroneDataPort.md) page explains how to copy video and flight log files from your drone to your computer.
- The [DataStore](./DataStore.md) page explains the spreadsheet used by the application to store data.
- The [Errors](./Errors.md) page describes all known error sources & how they are minimised. 
- The [Ground](./Ground.md) page explains how detailed ground and treetop elevation data is obtained and displayed.
- The [Process](./Process.md) page explains the image processing options the application supports.
- The [ManualCategorisation](./ManualCategorisation.md) page explains how users manually categorise the animals detected.
- The [AutoCategorisation](./AutoCategorisation.md) page outlines the automation categorisation of some animals detected.


## Caveats
This tool has only been extensively tested with:
- Data from a DJI Mavic 2 Enterprise (M2E) Dual drone. SkyComb Analyst is designed to support any drone, but other drone models may require some code changes around flight log parsing and loading. Refer [Drone](./Drone.md) for more details.
- Data generated using the [Flight](./Flight.md) page data collection recommendations, especially: 1) the flight starts and ends on the ground and 2) the camera(s) are pointing straight down during the flight. SkyComb Analyst will support other flight configurations, but the height accuracy will be worse.  
- Ground (surface and treetop) data for New Zealand. SkyComb Analyst is designed to support any country, but supporting additional countries will involve locating & integrating publically-available Lidar data. Refer [Ground](./Ground.md) for more detail.

## Thanks
Thanks to Toitu Te Whenua (Land Information New Zealand) for providing detailed land elevation data.   
