# [SkyComb Analyst](https://github.com/PhilipQuirke/SkyCombAnalystHelp/blob/main/README.md) - Ground

## Overview
The SkyComb Analyst tool works better with accurate ground and tree-top elevation data.
This page covers how this elevation data is used in the application.
(Refer the root-level [ReadMe](./README.md) for an overview of the tool.)


## Ground Elevation
SkyComb Analyst tries to determine whether a heat source is at ground level or is located up in a tree, above the ground. 
For this, highly accuracy ground & surface (aka tree-top) elevation data is needed.

While the drone provides its own altitude and location, it can't provide information on the elevation of the ground or 
tree tops. For ground and tree-top elevations, an alternative input source is needed.


## Elevation Data Sources
Some countries publish ground elevation maps based on [LIDAR](https://en.wikipedia.org/wiki/Lidar) surveys, which have very 
accurate data, and can provide both ground elevation and also the height of the foliage above ground (aka surface elevation 
aka tree-top elevation). 

### New Zealand Elevation Data Sources
New Zealand is progressively mapping the entire country using LIDAR and publishing the data for free.
Current and planned coverage is summarised at https://www.linz.govt.nz/products-services/data/types-linz-data/elevation-data

The New Zealand government LINZ web site provides the ground data. For example:
- https://data.linz.govt.nz/layer/105089-auckland-north-lidar-1m-dsm-2016-2018/ a DSM (Digital Surface Model) data for Auckland, New Zealand.
- https://data.linz.govt.nz/layer/106410-auckland-north-lidar-1m-dem-2016-2018/ a DEM (Digital Elevation Model) data for Auckland, New Zealand.

After creating a (free) LINZ account, you can generate a (free) API key, allowing you to access this data for free.
The data is available in a grid of 1 meter by 1 meter (horizontal) squares with a elevation (vertical) accuracy of +/-0.2 meters.
This is a phenomenal level of accuracy, and SkyComb Analyst really benefits from this accuracy.

This data is used to draw 2D ground and surface contors in the [user interface](./UserInterface.md).
The data is also stored and graphed in the [DataStore](./DataStore.md) (aka spreadsheet) associated with each drone flight:

![Example Contor Graphs](./Static/Overview2.png?raw=true "Example Contor Graphs")


## Using "File Based" Elevation Data
The GroundSpace folder contains a "file based" method for obtaining elevations data in the SkyComb Analyst. 
This requires some set-up, then is very fast and very accurate. This method is highly recommended if you want to use SkyComb Analyst offline.

To set up this method, export (download) the ground (aka DEM) and surface (aka tree-top aka DSM) datasets from the LINZ (or similar) 
website in the "GeoTiff" format. LINZ has a 13Gb limit on individual exports. In the LINZ web site user interface you can manually reduce the area you want to export until it is under the 13b limit. 
As a rough guide a 10Gb GeoTiff export will cover some 4,000 km2. 

Set the GroundDirectory setting in App.Config to the root folder used to store this ground 
data e.g. D:\SkyComb\Ground_Data . Unzip each downloaded ZIP into a separate sub-folder of the GroundDirectory folder.

For example, exporting subsets of this Lidar data:
- Exported a 4.6 Gb subset of this dataset lds-auckland-north-lidar-1m-dem-2016-2018-GTiff.zip. It covered ~5,000 km2. 
- Exported a 4.7 Gb subset of this dataset lds-auckland-north-lidar-1m-dsm-2016-2018-GTiff.zip. It covered ~5,000 km2. 

The first time that the SkyComb Analyst is run after unzipping new datasets into the GroundDirectory folder, the tool automatically scans the subfolders, 
and creates an index (e.g. D:\SkyComb\Ground_Data\SkyCombIndexTiff.xlsx) containing names of all the Tiffs found and the ground area each covers. 
Subsequent SkyComb Analyst runs uses this index to quickly locate the Tiff files pertainent to any drone flight in that coverage area.

SkyComb Analyst also supports the ASC (text) format but this format is bulkier and slower. This format is *not* recommended. 


## Other Countries
The method is currently implemented for NZ, but is easily extensible to data sources from other countries.
Seach the source code for #ExtendGroundSpace to find what code to modify to support another country.


## Using "Cloud Based" Elevation Data
The SkyComb Analyst environment will in the future implement a cloud based version of the Ground source code, tentatively called SkyGround.
If you run the SkyComb Analyst tool on a video, and you don't have the elevation data available as files on your laptop, and you are online, 
the tool will automatically ask SkyGround to provide the elevation data.
