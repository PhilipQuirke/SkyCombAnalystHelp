# [SkyComb Analyst](https://github.com/PhilipQuirke/SkyCombAnalystHelp/blob/main/README.md) - Categorisation

# Overview
This page covers the manual categorisation of animals detected by the SkyComb Analyst tool.
(Refer the root-level [ReadMe](./README.md) for an overview of the whole tool.)


# Purpose
The SkyComb Analyst tool uses image processing to detect animals in a thermal video.
The user can manually categorise the animals detected, for reporting purposes.


# Category Forms 
After processing a thermal video, the list of detected animals is shown in the main form.
About this list are two "pop out" icons:
- The right one opens a form where you can edit the master categories.
- The left one opens the object explorer form. In this form you can label each object with one of the master categories.


# Master Categories
The "pop out" icon on the right above the objects list opens the "Master Categories" form. 
In this form, you can add, edit and delete the master categories.
These are the categories that can later be applied to individual detected animals.

Each master category has these fields:
- Category: The name of the Category. Must be unique.
- Include: States whether the category should included in various graphs and summarised. Set to "No" if the category is not of interest to you.
- Notes: General purpose text field

Clicking "Save" stores the master categories to the DataStore in tab "Cat1".

## Default Master Categories
The default set of master categories are:
- Animal
- Bird
- Cat
- Cow
- Dog
- Inanimate (Include = "No")
- Person (Include = "No")
- Pig
- Possum
- Stone
- Water

# Object Categories
The "pop out" icon on the left above the objects list opens the "Object Explorer" form. 
In this form, you can select an object and apply one of the master categories to it.
Applying a master category to an object also updates the Include and Notes fields with the Master Category values.

Clicking "Save" stores the object categories to the DataStore in tab "Cat2".

![Object Explorer](./Static/ObjectExplorer.png?raw=true "Object Explorer")

## Object Category Persistance
Suppose you set the category on several objects in Leg B, C and D and save these object categories to the DataStore.
Suppose you then reprocess the same video but only for Leg D. All the object categories for Legs B, C and D are still retained in the DataStore.
Suppose you then reprocess the same video yet again but this time for Legs B, C & D. All the object categories for Legs B, C and D will reappear in SkyComb Analyst.
 
The only way to remove an existing Object Category is to select the object in the Object Explorer and set the Category to blank, and then click Save.




