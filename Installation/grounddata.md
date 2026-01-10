# [SkyComb Analyst](https://github.com/PhilipQuirke/SkyCombAnalystHelp/blob/main/README.md) Ground Data etc Folders

## Overview
SkyComb Analyst uses (Lidar) ground contour data to determine the height above ground of detected animals. This page details how to install ground data for use in SkyComb Analyst. 

## Folders
SkyComb Analyst uses the following folders for ground data, input data, and output data. You can change these folders in the Preferences page in SkyComb Analyst - for example if you want to use C: instead of D:.

- D:\SkyComb\Data_Ground\     The lidar ground contour data files
- D:\SkyComb\Data_Input\      The input thermal video and image files
- D:\SkyComb\Data_Output\     The output SkyComb results files    

## Ground Data Folders
The lidar ground contour folder must contain a subfolder called nz-quasigeoid-2016-raster e.g.
- D:\SkyComb\Data_Ground\nz-quasigeoid-2016-raster

This folder must contain at least the file new_zealand_quasigeoid_2016_raster.tif which can be downloaded from:
- https://drive.google.com/drive/folders/1kBHiEwMqPzKbVxvk3hqdnQ1JYplDoRR0
The other files in the folder are not used but are included for completeness.

Lidar ground data can be downloaded from various sources including government data portals. The data needs to be in GeoTiff format. SkyComb staff may provide the data you. The following example files were provided to one user:

- D:\SkyComb\Data_Ground\lds-waikato-lidar-1m-dem-2021-GTiff\
- D:\SkyComb\Data_Ground\lds-waikato-lidar-1m-dsm-2021-GTiff\
- D:\SkyComb\Data_Ground\West-coast-lidar-1m-dem-2020-2025\
- D:\SkyComb\Data_Ground\West-coast-lidar-1m-dsm-2020-2025\
- D:\SkyComb\Data_Input\15Sep25Thermos\
- D:\SkyComb\Data_Input\15Sep25Pukeko\
