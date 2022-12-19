# [SkyComb Analyst - Ground](https://github.com/PhilipQuirke/SkyCombAnalystHelp/) 

# Overview
This ReadMe covers the purpose and content of the GroundSpace folder of the SkyComb Analyst application.
(Refer the root-level [ReadMe](./ReadMe.md) for an overview of the whole application.)


# Ground Elevation
SkyComb Analyst tries to decide whether a heat source is at ground level or is located up in a tree, above the ground. 
Highly accuracy ground & surface (aka tree-top) elevation data is needed.

While the drone provides its altitude and location, it can't provide information on the elevation of the ground or 
tree tops beneath it. For ground and tree-top elevations, alternative input sources are needed.


# Elevation Data Sources
Some countries publish ground elevation maps based on [LIDAR](https://en.wikipedia.org/wiki/Lidar) surveys, which have very 
accurate data, and can provide both ground elevation and also the height of the foliage above ground (aka surface elevation 
aka tree-top elevation). 

## New Zealand Elevation Data Sources
New Zealand is progressively mapping the entire country using LIDAR and publishing the data for free.
The New Zealand government LINZ web site provides the ground data. For example:
- https://data.linz.govt.nz/layer/105089-auckland-north-lidar-1m-dsm-2016-2018/ a DSM (Digital Surface Model) data for Auckland, New Zealand.
- https://data.linz.govt.nz/layer/106410-auckland-north-lidar-1m-dem-2016-2018/ a DEM (Digital Elevation Model) data for Auckland, New Zealand.

After creating a (free) LINZ account, you can generate a (free) API key, allowing you to access this data for free.
The data is available in a grid of 1 meter by 1 meter (horizontal) squares with a elevation (vertical) accuracy of +/-0.2 meters.
This is a phenomenal level of accuracy, and SkyComb Analyst really benefits from this accuracy.


# Using Elevation Data Sources
The GroundSpace folder contains two methods for using elevations data in the SkyComb Analyst:
- File based: Requires some set-up, then is very fast and very accurate. Recommended method.
- HTTPS: Requires minimal set-up, but is very slow, much less accurate and requires Internet access. 

Both methods are implemented for NZ data sources, but are easily extensible to data sources from other countries.
Seach the source code for #ExtendGroundSpace to find what code to clone & modify to support another country.

Both methods require you to gain access to an elevation data source. 
In New Zealand, you can create a (free) account at the LINZ website, then use it to generate a (free) API key, 
allowing you to access this data for free. Set the LinzApiKey setting in App.Config to your API key value.

## "File based" method requires some set up effort but is then very fast and very accuracy.
This approach allows a high-resolution ground grid (with 1m horizontally between data points), and fast runs. 
This is the recommended approach. 

To set up this method, download the ground (aka DEM) and surface (aka tree-top aka DSM) datasets from the LINZ (or similar) 
website in the "ASC" format. Set the GroundDirectory setting in App.Config to the root folder used to store this ground 
data e.g. D:\SkyComb\Ground_Data . Unzip each downloaded ZIP into a separate sub-folder of the GroundDirectory folder.

For example, the above datasets are downloaded as:
- lds-auckland-north-lidar-1m-dem-2016-2018-AAIGrid.zip is 11 GB when downloaded, and 40 GB once unzipped. 
- lds-auckland-north-lidar-1m-dsm-2016-2018-AAIGrid.zip is 12 GB when downloaded, and 43 GB once unzipped. 

The first time that the SkyComb Analyst is run after unzipping new datasets into GroundDirectory, the tool automatically scans the subfolders, 
and creates a datastore (e.g. D:\SkyComb\Ground_Data\SkyCombIndex.xlsx) containing names of all the ASC datasets found and the area each covers. 
Subsequent SkyComb Analyst runs uses this index to quickly locate the ASC files pertainent to any drone flight in that coverage area.


## The "HTTPS" method requires less set-up, but is very slow, much less accurate and requires Internet access
You can use test your API key using any browser to access their Web Tile and Raster query APIs on-demand. For example:
- https://data.linz.govt.nz/services/query/v1/raster.json?key=Your_API_Key_Here&layer=105089&x=174.7679000000037&y=-36.85059999999978 for DSM data
- https://data.linz.govt.nz/services/query/v1/raster.json?key=Your_API_Key_Here&layer=106410&x=174.7679000000037&y=-36.85059999999978 for DEM data

While convenient, accessing elevation data this way is slow. Further LINZ imposes a limit of ~100 sequential queries. 
After this it starts rejecting some queries. The limit of 100 queries results in SkyComb using a low-resolution ground 
grid (with say 38m horizontally between data points). This is suboptimal. 
