# [SkyComb Analyst](https://github.com/PhilipQuirke/SkyCombAnalystHelp/blob/main/README.md) - Automatic Categorisation

## Overview
This page covers the *automatic* categorisation of animals detected by the SkyComb Analyst tool.
The [ManualCategorisation](./Category.md) has an overview of the manual categorisation of animals.
The main [ReadMe](./README.md) has an overview of the whole tool.


## Purpose
SkyComb Analyst supports manual categorisation of detected animals, but automatic categorisation is preferred.

Automatic categorisation (auto-cat) is hard. But it is a problem that can be solved a piece at a time. 
Auto-cat is an area of ongoing research for SkyComb Analyst. This page describes the approaches and rationale.


## Partial auto-cat
In a perfect world, SkyComb Analyst would identify the species of all animals detected in a flight. This seems unachievable. 

If SkyComb Analyst can successfully identify the species of *some* of the animals detected:
- Manual categorisation can be applied to the unidentified animals. 
- Good population estimates with error ranges can be calculated. 
- If needed, additional flights can add extra data 

Partial auto-cat is acheivable using a number of useful partial solutions / characterisations:
- Predator Free 2050 has a goal of eliminating some NZ pest species by 2050. Differentiating between pest and on-pest species is useful.
- Animal locomotion characteristics - does the animal have 2 or 4 lege? Do they walk or hop?
- For an active / moving animal, the time of day the video was taken can exclude / include some animal species.  
- The location being at-ground-level vs above-ground-level is a useful differentiator
- Animal size is a useful differentiator
- Animal temperature may be a useful differentiator. 
- Animal colour is sometimes a useful differentiator. 
- Animal "eye shine" colour. 
- Compound images


## Definition of Pest in New Zealand
In New Zealand (NZ), farms contain introduced ( *exotic* ) mammal species including sheep, cattle, pigs, deer, cats & dogs. NZ's only native mammal is a bat. So NZ has no *native* cat, dog, sheep, pig, cattle, deer, horse, possum, rat, ferret, stoat, hedgehog, rabbit or wallaby species. Most NZ animal species are birds.

In conservation land *all* mammals (except bats) are exotic pests. Mammals have some charateristics that easily differentiate them from birds and bats. SkyComb Analyst can leverage these characteristics.


## Mammal Locomotion
For some detected animals, image processing can automatically detect "locomotion" characteristics:
- On NZ conservation land, if a (thermal or optical) video shows an animal walking on 4 legs or hopping on 2 legs it is a pest mammal. 
- On NZ farmland, any hopping mammal is a pest. 

Mammal locomotion is best seen in videos when the mammal is walking on the ground. Some mammals climb trees, but walking across atree branch is hard to see. Also the mammal may not be moving at all. So this is a partial solution.


## Time of Day
Most species are nocturnal (active at night) or diurnal (active during the day) but not both.  

For an active / moving animal, the time of day the video was taken can exclude / include some animal species.  


## Height above Ground
Some species, such as cows, do not climb trees.

If an animal is located say 4 meters above the ground, some animal species can be excluded / included.  


### Mammal Size
In NZ, a mammal larger than a certain size is a cow, deer or horse. NZ has no bears, tigers, hippos, etc. Size is a useful distinction that SkyComb Analyst can automatically apply to exclude / include some species from consideration. 

On a given farm, the smallest non-pest animal will be a cat, dog or sheep. Any walking mammal smaller than this limit is a pest - either a rat, stoat, ferret, hedgehog, possum, rabbit or wallaby.  


## Animal Temperature
Each animal species has its own "normal" temperature range. For a diurnal species there will be a different temperature range for the daytime (when they are active) and the nighttime (when they are sleeping).  

Depending on the time of day the video was taken, and the animal temperature, some animal species can be excluded / included.

More research is needed in this area.


## Animal Colour
For drones that have both thermal and optical cameras, an optical image of the animal may be visible.  

In NZ, the only common animal that is >90% white in colour is the sheep.

Various breeds of cows have a distinctive colour pattern e.g. A Friesen cows are black and white  


## Animal eye-shine colour
For drones that have both thermal and optical cameras, an optical image of the animal may be visible.  

In low-light / night-time conditions, various species of animal have different 'eye-shine' colours. 
For example, possums' eye-shine is red-orange, rabbits' is red-pink, sheep and cattle is yellow-green.

Some nocturnal animals look towards light sources e.g. possums.


## Compound images
Many detected animals will be largely covered by foilage. But the foliage does not completely cover the animal. 
Each thermal camera pixel that "fires" indicates a (small, temporary) gap in the foilage opening a direct path from part of the animal to the thermal camera.

The animal can cause a series of pixels to fire in a physically concentrated area of the thermal image over a sequence of video frames.
When the density of firing pixels both by image area and time sequence passes a threshold the animal is detected.

If the drone also has an optical camera, the optical camera will have say 8 times as many pixels as the thermal camera. 
So for each thermal camera pixel there are say 8 corresponding optical camera pixels pointing at the same place. 

It is possible to assemble a single *optical* "compound image" of the animal from the multiple frames it was detected in.
The image is assembled by using the "peak" thermal pixels in each frame, and using the optical pixels associated with the peak thermal pixels.

More research is needed in understand the usefulness of this compound image in animal species detection.
