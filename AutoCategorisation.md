# [SkyComb Analyst](https://github.com/PhilipQuirke/SkyCombAnalystHelp/blob/main/README.md) - Automatic Categorisation

## Overview
This page covers the *automatic* categorisation of animals detected by the SkyComb Analyst tool.
The [ManualCategorisation](./ManualCategorisation.md) page has an overview of the manual categorisation of animals.
The main [ReadMe](./README.md) has an overview of the whole tool.


## Purpose
SkyComb Analyst supports manual categorisation of detected animals, but automatic categorisation is preferred.

Automatic categorisation (auto-cat) is hard. But it is a problem that can be solved a piece at a time. 
Auto-cat is an area of ongoing research for SkyComb Analyst. This page describes the approaches and rationale.


## Partial auto-cat
Given that SkyComb Analyst will most likely only auto-cat *some percentage* of the animals detected in a flight:
- Manual categorisation can be applied to the unidentified animals. 
- Good population estimates with error ranges can be calculated for the flight area. 
- If needed, additional flights can add extra data in the same area.


## Partial auto-cat implementation
Partial auto-cat is achievable using a number of useful partial solutions / characterisations:
- Predator Free 2050 has a goal of eliminating some NZ pest species by 2050. Differentiating between pest and non-pest species is useful.
- Animal shape characteristics e.g. does the animal have 2 or 4 legs? 
- Animal locomotion characteristics e.g. does the animal walk or hop?
- For an active / moving animal, the time of day the video was taken can exclude / include some  animal species.  
- The animal location being at-ground-level vs above-ground-level is a useful differentiator. Pigs don't climb trees.
- Animal size is a useful differentiator.
- Animal movement speed is a useful differentiator.
- Animal temperature may be a useful differentiator. 
- Animal heat patterns is a useful differentiator. 
- Animal colour / colour pattern is sometimes a useful differentiator. 
- Animal "eye shine" colour may be a useful differentiator.  
- Compound optical images may be useful for distinguishing between fur vs feathers.

For a given animal, SkyComb Analyst will, where feasible, evaluate the above characterisations. 
For some percentage of animals detected, from this information, a Machine Learning (ML) "decision tree" will be able to identify the animal's species. 
If not, the model can evaluate the probability that the animal belongs to various species.


## Useful animal characterisations
In more detail, these are the characterisations that may be useful in identifying a given animal's species:


### Definition of Pest in New Zealand
In New Zealand (NZ), farms contain introduced ( *exotic* ) mammal species including sheep, cattle, pigs, deer, cats & dogs. NZ's only native mammal is a bat. So NZ has no *native* cat, dog, sheep, pig, cattle, deer, horse, possum, rat, ferret, stoat, hedgehog, rabbit or wallaby species. Most native NZ animal species are birds and insects.

In conservation land *all* mammals (except bats) are exotic pests. Mammals have some characteristics that easily differentiate them from birds and bats. SkyComb Analyst can leverage these characteristics.


### Animal Shape
For some detected animals, image processing can automatically detect useful "shape" characteristics. For example, an animal with 3 or 4 legs visible in an image is a mammal. The legs of a mammal may not be visible, so this is a partial solution.


### Animal Locomotion
For some detected animals, image processing can automatically detect "locomotion" characteristics:
- On NZ conservation land, if a (thermal or optical) video shows an animal walking on 4 legs or hopping on 2 legs it is a pest mammal. 
- On NZ farmland, any hopping animal is a pest. 

Animal locomotion is best seen in videos when the animal is walking on the ground or along a branch. The animal may not be moving at all. So this is a partial solution.


### Time of Day
Most species are either nocturnal (active at night) or diurnal (active during the day) but not both.  

For an active / moving animal, the time of day the video was taken can exclude / include some animal species.  


### Height above Ground
Some species, such as cows, do not climb trees.

If an animal is located say 4 meters above the ground, some animal species can be excluded / included.  


### Animal Size
An animal over a certain size is not a bird. 

In NZ, a mammal larger than a certain size is a cow, deer or horse. NZ has no bears, tigers, hippos, etc. Size is a useful distinction that SkyComb Analyst can automatically apply to exclude / include some species from consideration. On a farm, the smallest non-pest mammal will be a cat, dog or sheep. Any walking mammal smaller than this limit is a pest - either a rat, stoat, ferret, hedgehog, possum, rabbit or wallaby.  


### Animal Movement Speed
Birds move fast when flying. When they are not flying, birds move slowly. An animal moving at an intermediate speed *between* these two speeds is not a bird. 

An animal, that is above ground level, slowly moving horizontally must be walking along a branch. It is likely *not* a bird, and in NZ is therefore likely a mammal.  


### Animal Temperature
Each animal species has its own "normal" temperature range. 
For a diurnal species there will be a different temperature range for the daytime (when they are active) and the nighttime (when they are sleeping). 
Similarly for nocturnal species. 

Depending on the time of day the video was taken, and the animal temperature, some animal species can be excluded / included.

More research is needed in this area.


### Animal Heat Patterns
Some animal species have a distinct heat pattern:
- A sheep's head and feet are visibly hotter than its body. This is different from a cow or possum.
- A peacock sitting on a tree branch has a very distinct heat pattern.

More research is needed in this area.


### Animal Colour / Colour Pattern
For drones that have both thermal and optical cameras, an optical image of the animal may be visible.  

In NZ, the only common animals that are >90% white in colour are sheep, goats, horses & llama.

Various breeds of cows have a distinctive colour pattern e.g. Friesen cows are black and white  


### Animal eye-shine colour
For drones that have both thermal and optical cameras, an optical image of the animal may be visible.  

In low-light / night-time conditions, various species of animal have different 'eye-shine' colours. 
For example, possums' eye-shine is red-orange, rabbits' is red-pink, sheep and cattle is yellow-green.

Some nocturnal animals look towards light sources making eye-shine colour easier to detect e.g. possums.


### Compound images
Many detected animals will be largely covered by foliage. But the foliage does not completely cover the animal. 
Each thermal camera pixel that "fires hot" indicates a (small, temporary) gap in the foliage opening a direct path from part of the animal to the thermal camera.

The animal can cause a series of pixels to fire in a physically concentrated area of the thermal image over a sequence of video frames.
When the density of firing pixels both by localised image area and time sequence passes a threshold SkyComb Analyst detects the animal.

If the drone also has an optical camera, the optical camera will have say 8 times as many pixels as the thermal camera. 
So for each thermal camera pixel there are say 8 corresponding optical camera pixels pointing at the same physical location. 

It is possible to assemble a single *optical* "compound image" of the animal from the multiple frames it was detected in.
The image is assembled by using the "peak" thermal pixels in each frame, and using the optical pixels associated with the peak thermal pixels.

More research is needed in understand the usefulness of this compound image in animal species detection.
It might for example be good enough to distinguish between fur and feathers.


## Decision Tree
SkyComb Analyst needs high quality data on NZ animal species characteristics (size, temperature range, nocturnal/diurnal, climber, etc) aligned to PF2050 goals.

For a given animal in a given video some (but not all) of the above methods will be applicable, giving some characteristics about the animal. 
Once SkyComb Analyst has access to NZ animal species characteristics data, it will apply a decision tree based on that characteristics data to (sometimes) definitively identify the animal species. 
Where the animal species can not be identified, SkyComb Analyst will be able to say "the animal is one of these 3 categories" with percentage likelihoods.

This is an area for research.


## Population Estimates
Once SkyComb Analyst can definitely identify the species of a percentage of the animals detected, and give species-probability distributions for the other animals. it can generate a population distribution estimate.

One factor in this estimate is how deeply through the foliage the thermal camera can detect animals. This is an area for research. 

SkyComb leverages high-accuracy metre-by-metre ground and surface (aka tree-top) data from LINZ. So it knows the depth of the ground cover, and can calculate the fraction of the depth of ground cover successfully searched by the thermal camera. This will aid in the population distribution estimation.


## Machine Learning
Machine Learning (ML) is a subset of Artificial Intelligence (AI). 
ML techniques can be used to create an algorithm to answer the question "What species is this animal?". 
It needs a "training set" of questions which already have correct answers (provided by humans).  

SkyComb needs training data specific to our use cases. This training data does not exist today in sufficient volume.

Enthusiastic volunteer conservations could help SkyComb Analyst build this training data.
An online tool will be built to ask a volunteer to categorise say 20 randomly-selected animals each day: 
- We will ask them to categorise some animals that SkyComb Analyst auto-categorised using the Decision Tree - to double-check the automatic categorisation accuracy.
- We will ask them to categorise some animals that SkyComb Analyst could not auto-cat. A person may be able to detect additional characteristics e.g. the shape of a bird's nest and the heat pattern from centre to edge may be a clear differentiator for them between a bird and a mammal. If multiple people agree on the categorisation of the animal, the categorisation is accepted, and the training data set size increases.

Over time, a database of categorised animals is built up. This is the additional training data that can be used to create a Machine Learning algorithm. This algorithm should then increase the percentage of animals that SkyComb Analyst can auto-categorise.
