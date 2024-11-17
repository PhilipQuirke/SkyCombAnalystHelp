# [SkyComb Analyst](https://github.com/PhilipQuirke/SkyCombAnalystHelp/blob/main/README.md) - Ground Elevation Source Data

## Overview
The SkyComb tool requires accurate ground and tree-top elevation data, for example, so it can calculate animal "height above ground" data.
This page covers where this elevation data is obtained.

## Drone Data
While the drone provides its own altitude and location, it can't provide information on the elevation of the ground or 
tree tops. For ground and tree-top elevations, an alternative input source is needed.

## NZ Elevation Data
Some countries publish ground elevation maps based on [LIDAR](https://en.wikipedia.org/wiki/Lidar) surveys, which have very 
accurate data, and can provide both ground elevation and also the height of the foliage above ground (aka surface elevation 
aka tree-top elevation). 

New Zealand is progressively mapping the entire country using LIDAR and publishing the data for free.
Current and planned coverage is summarised at https://www.linz.govt.nz/products-services/data/types-linz-data/elevation-data

The data is available in a grid of 1 meter by 1 meter (horizontal) squares with a elevation (vertical) accuracy of +/-0.2 meters.

The New Zealand government LINZ web site provides the ground data. For example:
- https://data.linz.govt.nz/layer/105089-auckland-north-lidar-1m-dsm-2016-2018/ a DSM (Digital Surface Model) data for Auckland, New Zealand.
- https://data.linz.govt.nz/layer/106410-auckland-north-lidar-1m-dem-2016-2018/ a DEM (Digital Elevation Model) data for Auckland, New Zealand.

This data is used to draw 2D ground and surface contors in the [user interface](./UserInterface.md).
The data is also stored and graphed in the [DataStore](./DataStore.md) associated with each drone flight.

## Using "File Based" Elevation Data
The SkyCombGroundLibrary code repository contains a "file based" method for obtaining elevations data. 
This requires some set-up, but then it is fast and accurate. 

This method is necessary if you want to use SkyComb tools offline. 
If you load the necessary ground data onto your laptop beforehand, you can process drone flight files on your laptop in the wild (without internet connectivity).

To do this, export (download) the ground (aka DEM) and surface (aka tree-top aka DSM) datasets from the LINZ (or similar) 
website in the "GeoTiff" format, covering the area you are interested in. LINZ has a 13Gb limit on individual exports. 
In the LINZ web site user interface you can manually reduce the area you want to export until it is under the 13b limit. 
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

