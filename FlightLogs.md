# [SkyComb Analyst](https://github.com/PhilipQuirke/SkyCombAnalystHelp/blob/main/README.md) - Flight Logs 


## Overview
The SkyComb Analyst tool helps environmentalists, conservationalists & scientists use a drone as a scientific tool.

The page summarises the information created by some drone models during flights and saved to their "flight log".

**Disclaimer**: This page is based on examples seen. Possibly the drone mentioned have additional capabilities that need to be enabled. 


## DJI Mavic 3t
This drone:
- Has a thermal camera, that supports change in focal length
- Records the Yaw, Pitch and Roll of the **camera** (not drone). This is positive for SkyComb Analyst. As the camera is on a stabilised gimbal, the Roll is normally zero. 
- **Does** allow the thermal camera focal length to be changed.
- Takes 30 thermal images / second

This is a sample entry from a DJI Mavic 3t thermal flight log named "DJI_20230628182818_0001_T.SRT" : 

<code>28115
00:15:37,683 --> 00:15:37,717
<font size="28">FrameCnt: 28115, DiffTime: 34ms
2023-06-28 18:43:56.810
[focal_len: 40.00] [dzoom_ratio: 1.00], [latitude: -37.996099] [longitude: 177.035704] [rel_alt: 75.645 abs_alt: 227.888] [gb_yaw: 76.8 gb_pitch: -49.1 gb_roll: 0.0] </font> </code>

## DJI M300 with XT2 19mm
This drone:
- Has a thermal camera, that supports change in focal length 
- Has a very brief SRT 
- Does allow the thermal camera focal length to be changed.
- Takes 30 thermal images / second

This is a sample entry from a DJI M300 with XT2 19mm thermal flight log named "DJI_0002.SRT" : 

  405
  00:06:44,000 --> 00:06:45,000
  2023.08.07 20:10:01
  GPS(-41.3899,174.0177,0.0M) BAROMETER:97.7M


## DJI Mavic 2 Enterprise (M2E)
This drone (new in ~2020):
- Has both a thermal and optical camera. So it creates two videos and two flight logs per flight. 
- Records the Yaw, Pitch and Roll of the **drone body** (not the camera). The camera is on a stabilised gimbal and so may be pointing in a different direction to the drone. This is negative for SkyComb Analyst
- Does **not** allow the thermal camera focal length to be changed.
- Takes 8 thermal images / second

This is a sample entry from a DJI Mavic M2E thermal flight log named "DJI_0094.SRT" : 

  4
  00:00:00,341 --> 00:00:00,455
  <font size="36">FrameCnt : 4, DiffTime : 114ms
  2022-09-08 06:26:55,549,370
  [color_md : default] [latitude: -36.885326] [longtitude: 174.697242] [altitude: 28.736000] [Drone: Yaw:-146.0, Pitch:-0.6, Roll:1.3] </font>


