# [SkyComb Analyst](https://github.com/PhilipQuirke/SkyCombAnalystHelp/blob/main/README.md) - Drone Data Port


## Overview
During a drone flight, while the drone is recording, it stores the new video and flight log data on an internal memory stick.  
This page covers how accesss this data.
(Refer the root-level [ReadMe](./README.md) for an overview of the whole application.)


## Drone Data Port
Your drone probably has a physical data port. For the Mavic 2 Enterprise it is here:

![Data Port Shut](./Static/DroneDataPortShut.jpg?raw=true "Data Port Shut")

You can open the cover to reveal the USB port. The actual type of USB connection may differ per drone:

![Data Port Open](./Static/DroneDataPortOpen.jpg?raw=true "Data Port Open")

For the Mavic 2 Enterprise it is a USB C connector. You will need a cable to connect the drone to your computer:

![USB C Cable](./Static/DroneDataUsbCable.png?raw=true "USB C Cable")

After connecting the drone data port to your computer using the USB cable, you can access the drone internal memory stick just like another other memory stick.
That is you can use your favourite file explorer tool to view and copy the files.

For some drones, the memory stick will not appear on your computer until *after* you power *on* the drone. 

After you have copied the files, remove the cable and remember to close the data port cover (in case your drone gets rained on later).


## Drone SD Card
Some drones have a removable SD Card (aka memory card) that the drone stores new video and flight log data on.

In this case, after physically removing the SD Card from the drone, you can use an SD Card Reader to copy the memory card contents onto your computer:

![SD Card Reader](./Static/SDCardReader.png?raw=true "SD Card Reader")

Remember to place the SD Card back into the drone afterwards. 


## Drone Data Files
The naming of drone data files depends on your drone model and whether it has one or two cameras. 

For the Mavic 2 Enterprise, which has a thermal and an optical camera, a single recording creates 4 files:

![Drone Data Files](./Static/DroneDataFiles.png?raw=true "Drone Data Files")

The four files have similar (but not exactly the same) creation date / times:
- The largest file is the optical video.
- The second largest file is the thermal video.
- The two small files are the flight logs - one for each video.

The two file logs were created at the same time during the same flight, so they share (duplicate) a lot of flight data, but there are differences between them:
- Each log contains data for each video frame, and the thermal and optical cameras have different frame rates, so the optical flight log contains more data.
- An optical camera has more "attributes" (such as FStop) than a thermal cmamera, so again the optical flight log contains more data.

It is recommended that you copy the files off your drone and onto your computer before processing them. Once this is done, the drone can be switched off. 

If they are available, SkyComb Analyst uses all 4 drone data files.
SkyComb Analyst can also process 2 files or just 1 video file, but fewer files means less data, and so fewer SkyComb Analyst features are available with fewer drone data files.   


## The DJI Drone flight log (.SRT) files are missing
Is your DJI drone creating video files (.MP4) but *not* creating any flight log (.SRT) files? This is likely a settings issue.

To enable the creation of the .SRT flight logs, in the DJI Go App:
- Choose the MENU option on the right side of the screen for Images and Video
- Choose the Video icon and ensute the file type is .MP4 (not .MOV)
- Choose the Option tool icon and turn the "Video Caption" setting *on*

With that option turned on, the .SRT files should be saved along with the .MP4 video file on your SD card when you record during a flight.
