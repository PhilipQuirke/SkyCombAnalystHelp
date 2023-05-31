# SkyComb Analyst Help

## Introduction
The SkyComb Analyst tool processes data collected by drones equipped with thermal and optical video cameras. It detects animals:

![FlightPathForm](./Static/DroneFlightPathForm.png?raw=true "Flight Path Form")

For each animal detected it shows their size, temperature & height above ground. 
It generates (thermal & optical) close up videos of each animal.
You can category the animals and exclude objects you are not interested in.

![Object Explorer](./Static/ObjectExplorer.png?raw=true "Object Explorer")

Drones are complex tools that move in three dimensions. The data they generate contains many inaccuracies. If you follow the SkyComb Analyst [recommendations](./Flight.md) on how to fly your drone, SkyComb Analyst can automatically compensate for [several inaccuracies](./Errors.md)

Where it is available, SkyComb Analyst supplements the drone data with very accurate ground and tree top **elevation** data from public sources, increasing the accuracy of **animal height above ground** estimates.

![DEM & DSM Elevations](./Static/Overview2.png?raw=true "DEM & DSM Elevations")

SkyComb Analyst automatically finds animals in the area flown over, in a robust and repeatable fashion. You can easily view each animal found. The tool generates [spreadsheets](./DataStore.md) and annotated video as output. This output supports further offline analysis e.g. as input to image recognition machine learning systems.

SkyComb Analyst provides an easy to use [interface](./UserInterface.md) that makes it easy to explore the data your drone collected.

![User Interface](./Static/UIExample.png?raw=true "User Interface")


## Index
These pages provide more detail:
- The [Flight](./Flight.md) page explains how to fly your drone missions to collect high-quality data.
- The [UserInterface](./UserInterface.md) page explains how to use the SkyComb Analyst tool to analyse your drone flight data. 
- The [Drone](./Drone.md) page explains aspects of the drone and drone-related source code.
- The [DroneDataPort](./DroneDataPort.md) page explains how to copy video and flight log files from your drone to your computer.
- The [DataStore](./DataStore.md) page explains the spreadsheet used by the application to store data.
- The [Errors](./Errors.md) page describes all known error sources & how they are minimised. 
- The [Ground](./Ground.md) page explains how detailed ground and treetop elevation data is obtained and displayed.
- The [Process](./Process.md) page explains the image processing options the application supports.
- The [Category](./Category.md) page explains how users manually categorise the animals detected.


## Caveats
This tool has only been extensively tested with:
- Data from a DJI Mavic 2 Enterprise (M2E) Dual drone. SkyComb Analyst is designed to support any drone, but other drone models may require some code changes around flight log parsing and loading. Refer [Drone](./Drone.md) for more details.
- Data generated using the [Flight](./Flight.md) page data collection recommendations, especially: 1) the flight starts and ends on the ground and 2) the camera(s) are pointing straight down during the flight. SkyComb Analyst will support other flight configurations, but the height accuracy will be worse.  
- Ground (surface and treetop) data for New Zealand. SkyComb Analyst is designed to support any country, but supporting additional countries will involve locating publically available ground data, and parsing and loading that data. Refer [Ground](./Ground.md) for more detail.
