#﻿Spotsizer2 manual
stephan.kamrad@crick.ac.uk

**General usage:**
spotsizer2 <run_mode> 
The current modes are:
mode | description
-----|------------
cfuq | Determine if a colony is present at each grid position
batch | Determine area and integrated density for each colony. For each image, analyse individually and create a csv
timecourse | Determine integrated density for each colony. Use the last image to create the mask and apply this to all previous images. Create a single csv as output.

**Spotsizer2 will always analyse all images in the current directory. The directory also needs to contain a Colonyzer.txt file with grid information and a spotsizer2.config file.**
The options in the spotsizer2.config file are the following:
Name|Description|Type|Default
----|-----------|----|-------
parallelQ|Should spotsizer2 use multiple CPU cores?|Boolean|TRUE
distanceThreshold|The distance between two grid positions will be divided by this number to compute the maximum distance a putative colony can be away from its reference grid position. Decreasing this number towards 2 makes colony-to-grid-matching more permissive (might help when your plate is at a slight angle).|float > 2|4
imageThreshold|"By default| the intensity threshold to distinguish colonies from background is determined by the Otsu method. The determined value will be multiplied by image_threshold to give the final threshold."|float > 0|1
sizeThreshold|Detected putative colonies will be filtered by size and small components (usually image noise) will be excluded. The default threshold is the image width divided by 32 and it is therefore independent of scanning resolution. This default is then multiplied by size_threshold to give the final threshold.|float > 0|1
negateQ|Should the image be colour inverted before processing? Images acquired with transmission scanning will generally require this. This option does not apply to cfuq_john |Boolean|TRUE
