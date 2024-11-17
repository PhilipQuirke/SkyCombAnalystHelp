# [SkyComb Analyst](https://github.com/PhilipQuirke/SkyCombAnalystHelp/blob/main/README.md) - Object Explorer

## Overview
After processing a thermal video, the home page shows the detected objects in a list at bottom right. 
The "pop out" icon abaove this list opens the Object Explorer:

![Object Explorer](./Static/ObjectExplorer.png?raw=true "Object Explorer")

## Object Explorer Areas
The Object Explorer page has these areas:

### Object List
At left, the list of the detected objects is shown. 
Each object is give a name (e.g. "C6") The name reflects the Flight Leg and the order the objects were detected in.   
Click on an list row to focus on that object.

### Object Detail
This area shows the size, "height above ground", when the object was first seen, how long it was seen for, its location, etc.
The user can manually assign the object an Object Category. Clicking Save saves the category and notes. 

### Object Image
This area shows an blown-up video showing just the object detected. The video cycles through the frames the object was seen in.

### Full Image
This area show the full video image. The object location is shown in red. Objects are shown in orange.

### Location
This area show the accuracy of the object location. It cycles through the frames the object was seen in. 
At each frame the object's estimated location is shown in orange. The best estimate is shown in red.

### Height
This area show the accuracy of the object "height above ground". It cycles through the frames the object was seen in. 
At each frame the object's estimated height is shown in orange. 
The longer the object is seen the more accurate the height calculation becomes.

### Frames
This area show detail related to each frame the object was seen in. 
The "Play" button can be used to pause / start this page cycling through the frames.

## Object Categories
The default master categories can be configured in a separate window shown below on the left:

![Animal Sizes](./Static/AnimalSizes.png?raw=true "Animal Sizes")

Notes:
- Terrestrial means that the object is restricted to the surface - that is it can not fly or climb trees.
- The min/max sizes are based on the SkyComb Analyst use case where we are detecting animals in the wilderness from above.    

## Object Category Persistance
Suppose you set the category on several objects in Leg B, C and D and save these object categories to the DataStore.
Suppose you then reprocess the same video but only for Leg D. All the object categories for Legs B, C and D are still retained in the DataStore.
Suppose you then reprocess the same video yet again but this time for Legs B, C & D. All the object categories for Legs B, C and D will reappear in SkyComb Analyst.
 
The only way to remove an existing Object Category is to select the object in the Object Explorer and set the Category to blank, and then click Save.
