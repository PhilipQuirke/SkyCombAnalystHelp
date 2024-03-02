# [SkyComb Analyst](https://github.com/PhilipQuirke/SkyCombAnalystHelp/blob/main/README.md) - Flight Logs 


## Overview
The SkyComb Analyst tool helps environmentalists, conservationalists & scientists use a drone as a scientific tool.

The page summarises the information created by some drone models during flights and saved to their "flight log".
Drone flight logs contain the Yaw, Pitch and Roll of the **drone body**. Some also record the Yaw, Pitch and Roll of the **camera** (not drone) - this helps SkyComb Analyst. As the camera is on a stabilised gimbal, the camera Roll is normally zero. 

**Disclaimer**: This page is based on examples seen. Possibly the drones mentioned have additional capabilities that need to be enabled. 


## DJI Mavic 3t
This drone:
- Has a thermal camera, that supports change in focal length
- Records the Yaw, Pitch and Roll of the **camera** (not drone).
- Takes 30 thermal images / second

This is a sample paragraph from a DJI Mavic 3t thermal flight log named "DJI_20230628182818_0001_T.SRT" : 

<code>28115
00:15:37,683 --> 00:15:37,717
<font size="28">FrameCnt: 28115, DiffTime: 34ms
2023-06-28 18:43:56.810
[focal_len: 40.00] [dzoom_ratio: 1.00], [latitude: -37.996099] [longitude: 177.035704] [rel_alt: 75.645 abs_alt: 227.888] [gb_yaw: 76.8 gb_pitch: -49.1 gb_roll: 0.0] </font></code>


## DJI M300 with XT2 19mm
This drone:
- Has a thermal camera, that supports change in focal length 
- Takes 30 thermal images / second

This is a sample paragraph from a DJI M300 with XT2 19mm thermal flight log named "DJI_0002.SRT" : 

<code>405
00:06:44,000 --> 00:06:45,000
2023.08.07 20:10:01
GPS(-41.3899,174.0177,0.0M) BAROMETER:97.7M</code>


## DJI Mavic 2 Enterprise (M2E)
This drone (new in ~2020):
- Has both a thermal and optical camera - creating two videos and two flight logs per flight. 
- Records the Yaw, Pitch and Roll of the **drone body** (not the camera). 
- Takes 8 thermal images / second

This is a sample paragraph from a DJI Mavic M2E thermal flight log named "DJI_0094.SRT" : 

<code>4
00:00:00,341 --> 00:00:00,455
<font size="36">FrameCnt : 4, DiffTime : 114ms
2022-09-08 06:26:55,549,370
[color_md : default] [latitude: -36.885326] [longtitude: 174.697242] [altitude: 28.736000] [Drone: Yaw:-146.0, Pitch:-0.6, Roll:1.3] </font></code>


## DJI M300 with H20T (T for Teddy) Camera 
This drone:
- Has a thermal camera.
- Records the Yaw, Pitch and Roll of **both** the drone body and the camera. 
- Takes 30 thermal images / second

This is a sample paragraph. Note the blank line in the middle. Note the use of the "font" delimiters in the SRT:

<code>
1
00:00:00,000 --> 00:00:00,033
< font size="28" >FrameCnt: 1, DiffTime: 33ms
2024-02-27 22:30:45.395
[fnum: 1.0] [focal_len: 58.00] [dzoom: 1.00] 
[latitude: -44.228828] [longitude: 171.193516] [rel_alt: 40.162 abs_alt: 97.829] 
[drone_speedx: 0.2 drone_speedy: 0.0 drone_speedz: 0.0] 
[drone_yaw: -20.4 drone_pitch: 2.4 drone_roll: -2.1] 
[gb_yaw: -30.0 gb_pitch: -29.9 gb_roll: 0.0] 

0
[dzoom_ratio: 10000, delta:0] [color_md : default] 
< /font >
</code>


## DJI M300 with H20N (N for Nancy) Camera
This drone:
- Has a thermal camera.
- Records the Yaw, Pitch and Roll of **both** the drone body and the camera. 
- Takes 30 thermal images / second

This is a sample paragraph. Note the blank line in the middle.Note the use of the "font" delimiters in the SRT:

<code>
1
00:00:00,000 --> 00:00:00,036
< font size="28" >SrtCnt : 1, DiffTime : 36ms
2024-02-28 00:13:26.240
[fnum: 1.0] [focal_len: 52.00] [dzoom: 1.79] 
[latitude: -44.228930] [longitude: 171.193573] [rel_alt: 40.050 abs_alt: 104.235] 
[drone_speedx: 0.5 drone_speedy: -0.1 drone_speedz: 0.0] 
[drone_yaw: -19.8 drone_pitch: -3.3 drone_roll: 0.0] 
[gb_yaw: -35.4 gb_pitch: -30.3 gb_roll: 0.0] 

0
[dzoom_ratio: 17871, delta:0] < /font >
</code>

