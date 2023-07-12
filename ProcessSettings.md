# [SkyComb Analyst](https://github.com/PhilipQuirke/SkyCombAnalystHelp/blob/main/README.md) Process Settings


## Overview
The Process Settings dialog allows you to configure setting related to image processing 


## Dialog Appearance
Click the "Process Settings" button in the main window opens the dialog to edit the image processing settings:

![Process Settings](./Static/ProcessSettings.png?raw=true "Process Settings")


## Dialog Settings


### Processing Algorithm
The [Process](./Process.md) page describes the supported image processing algorithms. 

If unsure, use the default setting "Comb".


### Processing Speed 
This setting takes values:
- **Slow** makes SkyComb Analyst pause momentarily after displaying each processed video frame  
- **Medium** is faster than slow
- **Fast** makes SkyComb Analyst run as fast as it can while still displaying each processed video frame
- **Max** makes SkyComb Analyst run as fast as it can while only displaying every hundreth processed video frame

If unsure, use the default setting "Fast".


### Gray scale "hot" threshold
Thermal image processing algorithms look at an image and categorise pixels as either "hot" (aka interesting) 
or "not hot" (aka uninteresting). The algorithm does this using a "hot threshold value" in the range 0 to 255. 

SkyComb Analyst can't automatically detect or calculate the "best" ThresholdValue.
You must calculate the best threshold value: 
- Too low a value and SkyComb Analyst will detect lots of "false hit" objects.
- Too high a value and SkyComb Analyst will not detect any objects.

Threshold Values as low as 150 and as high as 235 have been useful with various drone thermal videos.

To calculate the best threshold value for your video:
- Set the "Run speed" to "Fast". 
- Set the "Threshold value" to "220".
- Click "Run" & watch the thermal video, until you see a hot object detected that looks interesting. Note the time it appears.
- Halt the run by clicking "Stop"
- Set "From/To (Secs)" to a few seconds before the object was detected, to a few seconds after it was detected. 
- Try increasing the "Threshold value" to say "230". Click "Run" and watch the object. Was the object outline better defined?
- Try decreasing the "Threshold value" to say "210". Click "Run" and watch the object. Was the object outline better defined?
- Repeat this process until you are happy with the Threshold Value


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


## Dialog Buttons
The dialog contains these buttons:
- **Save** : Clicking writes the changes to the [DataStore](./DataStore.md) and closes the dialog. Button is only enabled after you make changes, and it shows the number of unsaved changes.
- **Undo** : Clicking reverse unsaved changes. Button is only enabled after you make changes, and it shows the number of unsaved changes.
- **Cancel** : Clicking closes the dialog. Button is not enabled if there are unsaved changes.
