# [SkyComb Analyst](https://github.com/PhilipQuirke/SkyCombAnalystHelp/blob/main/README.md) Process Settings


## Overview
The Process Settings dialog allows you to configure setting related to video image processing 


## Dialog Appearance
Click the "Process Settings" button in the main window opens the dialog to edit the video image processing settings:

![Process Settings](./Static/ProcessSettings.png?raw=true "Process Settings")


## Dialog Settings


### Processing algorithm
The [Process](./Process.md) page describes the supported image processing algorithms. 

If unsure, use the default setting "Threshold".


### Processing speed 
This settings applies to SkyComb Analyst but not to SkyComb Flights.

This setting takes values:
- **Slow** makes SkyComb Analyst pause momentarily after displaying each processed video frame  
- **Medium** is faster than slow
- **Fast** makes SkyComb Analyst run as fast as it can while still displaying each processed video frame
- **Max** makes SkyComb Analyst run as fast as it can while only displaying every hundreth processed video frame

If unsure, use the default setting "Fast".


### Pixel "hot" threshold (50 to 255)

Thermal images contain pixels with "heat" values in the range 0 to 255.

The processing algorithms find pixels as either "hot" (i.e. interesting) 
or "not hot" (i.e. uninteresting) using this "hot pixel threshold" setting. 

Theoretically this setting could be in the range 0 to 255, by in practice values below 50 are not useful. 

The default value of 200 is empirically found to be a good value for many DJI thermal cameras.
But the best value depends on the ambient temperature during the flight, and the type of animals being detected.


### Radio lower threshold (4000 to 5000)

SkyComb Analyst uses radiometric temperature values stored in thermal images created by DJI drones.
This setting defines the lower threshold for radiometric temperature values.
Any radiometric value below this setting is increased to this threshold.
Any radiometric value at (or below) this setting is "never interesting".

DJI thermal cameras encode radiometric temperature values in the range 4000 to 5000. 
The default of 4575 is empirically found to be a good value for many DJI thermal cameras.

SkyComb maps the radiometric temperature values linearly to "hot pixel values" in the range 0 to 255. This setting defines the "hot pixel" value 0.

### Radio upper threshold (4000 to 5000)

SkyComb Analyst uses radiometric temperature values stored in thermal images created by DJI drones.
This setting defines the upper threshold for radiometric temperature values.
Any radiometric value above this setting is reduced to this threshold.
Any radiometric value at (or above) this setting is "always interesting".

DJI thermal cameras encode radiometric temperature values in the range 4000 to 5000. 
The default of 4620 is empirically found to be a good value for many DJI thermal cameras.

SkyComb maps the radiometric temperature values linearly to "hot pixel values" in the range 0 to 255. This setting defines the "hot pixel" value 255.


### YOLO detect confidence (0.1 to 0.9)

This setting is specific to YOLO (You Only Look Once) image processing algorithm. 

If unsure, use the default setting 0.66


### YOLO intersection over union (0.1 to 0.9)

This setting is specific to YOLO (You Only Look Once) image processing algorithm. 

If unsure, use the default setting 0.25


### Max distance to detect features (50 to 250m)

When SkyComb detects an object, the SkyComb physics model estimates the distance away the object is from the drone.

If the distance is greater than this threshold then the object is ignored. The rationale is that to detect an object at a great distance, the object must be very large, and so it is not an animal. 

If unsure, use the default setting 150


### Save annotated video

SkyComb Analyst can create a video as output. This video mirrors what is shown in the main window of SkyComb Analyst. That is, it is a copy of the input video, overlaid with any objects detected. 

Use this setting to say whether an annotated video should be created.  If unsure, use the default setting "Yes".


### Saver object data

SkyComb Analyst creates a spreadsheet (aka [DataStore](./DataStore.md) ) of results. 

Use this setting to say whether object details should be saved to the spreadsheet. This setting takes values:
- **Significant** Only significant (aka interesting) detected objects are saved
- **All** All (significant and insignificant) detected objects are saved
- **No** No object data is saved

If unsure, use the default setting "Significant".


### Min # hot pixels in object (1 to 1000)

When detecting say possums, and given an operator's standard drone altitude, the operator may not empirically that a single hot pixel is too small to be an animal. 

This setting defines the minimum number of hot pixels that must exist in a tight cluster for the object to be considered significant (i.e. interesting).


## Dialog Buttons

The dialog contains these buttons:
- **Save** : Clicking writes the changes to the [DataStore](./DataStore.md) and closes the dialog. Button is only enabled after you make changes, and it shows the number of unsaved changes.
- **Undo** : Clicking reverse unsaved changes. Button is only enabled after you make changes, and it shows the number of unsaved changes.
- **Cancel** : Clicking closes the dialog. Button is not enabled if there are unsaved changes.
