# SkyComb Analyst Help

## Purpose
The SkyComb Analyst tool helps environmentalists, conservationists & scientists use a drone with a thermal video camera as a scientific tool 
to collect information on wild animal populations in an automated, robust, repeatable, cost-effective & safe way.

## Video Introduction
This 4 minute introductory video overviews the tool https://www.youtube.com/watch?v=QY1EAinyYJM . The product interface has improved since this video was made.

## Description
The SkyComb Analyst tool processes data collected by drones equipped with thermal video cameras. It detects animals:

![FlightPathForm](./Static/DroneFlightPathForm.png?raw=true "Flight Path Form")

For each animal detected it shows their size & height above ground. 
It generates close up images of each animal.
You can category the animals and exclude objects you are not interested in.

![Object Explorer](./Static/ObjectExplorer.png?raw=true "Object Explorer")

Drones are complex tools that move in three dimensions. The data they generate contains many inaccuracies. If you follow the SkyComb Analyst [recommendations](./Flight.md) on how to fly your drone, SkyComb Analyst can automatically compensate for [several inaccuracies](./Errors.md)

SkyComb Analyst supplements the drone data with very accurate ground and tree top **elevation** data from public (Lidar) sources, increasing the accuracy of **animal height above ground** estimates.

SkyComb Analyst automatically finds animals in the area flown over, in a robust and repeatable fashion. You can easily view each animal found. The tool generates [spreadsheets](./DataStore.md) and annotated video as output. This output supports further offline analysis.

SkyComb Analyst provides an easy to use [interface](./UserInterface.md) that makes it quick to explore the data your drone collected.

![User Interface](./Static/UIExample.png?raw=true "User Interface")


## Index of Content
These pages provide more detail on the tool and its use:
- The [HomePageControls](./HomePageControls.md) page explains the SkyComb Analyst home page controls.
- The [UserInterface](./UserInterface.md) page explains how to use the SkyComb Analyst tool to analyse your drone flight data.
- The [FlightLeg](./Flightleg.md) page explains the drone flight path term "Leg" and how SkyComb uses them.
- The [SizeCategory](./SizeCategory.md) page explains how SkyComb categorises animals by their size.
- The [HeightCategory](./HeightCategory.md) page explains how SkyComb categorises animals by their height above ground.
- The [ObjectExplorer](./ObjectExplorer.md) page explains how users explore the animals detected.

These pages provide more detail on drones and drone flights:
- The [Drone](./Drone.md) page explains drone terminology related to the SkyComb Analyst tool.
- The [Flight](./Flight.md) page explains how to fly your drone missions to collect high-quality data.
- The [DroneDataPort](./DroneDataPort.md) page explains how to copy video and flight log files from your drone to your computer.
- The [DataStore](./DataStore.md) page explains the spreadsheet used by the application to store data.
- The [Errors](./Errors.md) page describes all known error sources & how they are minimised. 
- The [Ground](./Ground.md) page explains how detailed ground and treetop elevation data is obtained and displayed.
- The [Process](./Process.md) page explains the image processing options the application supports.
- The [AutoCategorisation](./AutoCategorisation.md) page outlines the automation categorisation of some animals detected.


## Caveats
This tool has only been tested in New Zealand conditions. 
Supporting additional countries will involve locating & integrating publically-available Lidar data. Refer [Ground](./Ground.md) for more detail. 

## Thanks
Thanks to Predator Free 2050 ( https://pf2050.co.nz/ ) for their financial and other support. 
Thanks to Toitu Te Whenua (Land Information New Zealand) for providing detailed land elevation data.   
