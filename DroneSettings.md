# [SkyComb Analyst](https://github.com/PhilipQuirke/SkyCombAnalystHelp/blob/main/README.md) Drone Settings


## Overview
The Drone Settings dialog allows you to configure setting related to the drone and its flight.


## Dialog Appearance
Click the "Drone Settings" button in the main window opens the dialog to edit drone settings:

![Drone Settings](./Static/DroneSettings.png?raw=true "Drone Settings")


## Dialog Settings

### Use Video From / To (Seconds)
These editable settings show the portion of the video that will be image processed by SkyComb Analyst. 

The default settings are from the start of the first Leg to the end of the last Leg.


### Drone on ground at 
If your drone very accurately measures its height above ground then this setting can be skipped. 

Otherwise, use the "Drone on ground at" field to state when the drone was on the ground by selecting one of:
- **Start** : The drone was on the ground at the start of the video (only). 
- **End** : The drone was on the ground at the end of the video (only). 
- **Both** : The drone was on the ground at both the start and end of the video. (This gives the best accuracy).
- **Neither** : The drone was not on the ground at any point of the video. 
- **Auto** : Use this if you don't know the answer

Based on this setting, SkyComb Analyst can automatically refine inaccurate drone height data.

The main window includes a "Drone Altitude" chart that shows the ground elevation in brown, the tree-top height in green and drone altitude in blue.
This diagram shows the inaccurate drone altitudes for an example flight that started and ended on the ground.
The altitude graph this  flight are shown four times, demonstrating how the different "Drone on ground at" settings is used mitigate the inaccuracies. 

![On Ground At Examples](./Static/OnGroundAtExamples.png?raw=true "On Ground At Examples")


### Gimbal Pitch/Roll/Yaw available
Some drones store the **drone body** pitch, roll and yaw data in their flight logs. 
Alternatively, some (more modern &/or expensive) drones store the **camera gimbal** pitch, roll and yaw data in their flight logs. 

If SkyComb Analyst can detect that your drone stores gimbal data, this setting will be set to **Yes (Auto)** and you can skip this setting. 

Otherwise select one of the following "Gimbal Pitch/Roll/Yaw available" values:
- **Yes** : The drone flight log contains gimbal data 
- **No** : The drone flight log contains drone body data
- **Auto** : Use this if you don't know the answer

For DJI drones, gimbal data was introduced in DJI SDK 4.3 and is incorporated into at least these models:
- DJI Mavic Air 2
- DJI Mavic 2 Pro/Zoom
- DJI Phantom 4 Pro V2.0
- DJI Inspire 2
- DJI Matrice 200 series
- DJI Matrice 600 series


### Camera down angle (degrees)
The camera gimbal controls where the drone camera is pointing. This setting can be skipped if the "Gimbal Pitch/Roll/Yaw available" setting is **Yes** or **Yes (Auto)**  

Otherwise, you need to indicate where the camera has point for the bulk of the flight. Use the "Camera down (angle) setting as follows: 
- If the camera was pointing straight down during the flight, then enter "90" (not -90).
- If the camera was pointing straight forward (horizontally), then enter "0".
- If the camera was pointing half way between straight down and straight forward, then enter "45" (not -45).  
- Or some other sensible value between "0" and "90"


### Optical to Thermal Video Delay
If your drone has a thermal camera but no optical camera, skip this setting.

For some drone flights, the first frame of the thermal and optical videos may start at slightly different times (e.g. 0.3 seconds different) 
and the optical and thermal videos will be slightly out of sync.  
SkyComb Analyst needs the videos to be time synchronised.

The "Video delay (secs)" setting handles this difference and synchronises the videos. To tune this setting for your drone video:
1. Set the "Video delay (secs)" setting to 0 & click Save
2. Click "Process Settings", set the "Speed" setting to Fast & click Save
3. Click "Run" and watch both the thermal and optical videos at the same time. 
4. As the drone turns a corner, see if the thermal and optical video images start to "turn" at the same time. If they do, they are sychronized, and there is nothing more to do!
5. If the images do *not* turn the corner at the same time:
    - Click Stop
    - Increase or decrease "Video delay (secs)" by say +/= 0.1 seconds
    - Repeat Steps 3 & 4 until the videos sync up.


### Minimum / maximum thermal temperature (celcius)
If your drone does not have a thermal camera, skip these settings.

Depending on the thermal camera manufacturer and model, the camera will measure a a specific range of temperatures. 

Some thermal cameras have an additional setting that allows them to focus on a smaller range of temperatures. For example, the DJI Mavic 2 Enterprise has a "Gain Mode" setting. If this is set to "High" the gray scale image is restricted to temperatures in the range -10C to 140C. This setting appears under the "Menu > Spanner (aka Wrench)" area of the DJI Pilot app.

Use these settings to enter the minimum and maximum temperature that your thermal camera measured during the flight. If unsure, leave the default values "-10" and "140". 


## Dialog Buttons
The dialog contains these buttons:
- **Save** : Clicking writes the changes to the [DataStore](./DataStore.md) and closes the dialog. Button is only enabled after you make changes, and it shows the number of unsaved changes.
- **Undo** : Clicking reverse unsaved changes. Button is only enabled after you make changes, and it shows the number of unsaved changes.
- **Cancel** : Clicking closes the dialog. Button is not enabled if there are unsaved changes.
