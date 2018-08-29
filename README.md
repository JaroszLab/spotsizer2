## Spotsizer2 manual  

stephan.kamrad@crick.ac.uk  

**General usage:**  
spotsizer2 <run_mode>  
The current modes are:  

mode | description
-----|------------
cfuq | Determine if a colony is present at each grid position
batch | Determine area and integrated density for each colony. For each image, analyse individually and create a csv
timecourse | Determine integrated density for each colony. Use the last image to create the mask and apply this to all previous images. Create a single csv as output.
phloxinb | Analyse images of plates containing phloxin B which were acquired by reflective (flatbed) scanning. The redness of colonies is determined instead of the size. Otherwise similar to batch mode.

**Spotsizer2 will always analyse all images in the current directory. The directory also needs to contain a grid.txt file with grid information and optionally a spotsizer2.config file.**  
The grid.txt file must contain a singe line stating the number of rows, number of columns, x of top left colony, y of top left colony, x of bottom right colony, y of bottom right colony. This must be in the Mathematica Image coordinate system, which has its origin in the lower left corner.  
The following options can be set in the spotsizer2.config file. If a file with this name does not exist in the image directory, default options will be used.  

Name|Description|Type|Default
----|-----------|----|-------
parallelQ|Should spotsizer2 use multiple CPU cores?|Boolean|True
distanceThreshold|The distance between two grid positions will be divided by this number to compute the maximum distance a putative colony can be away from its reference grid position. Decreasing this number towards 2 makes colony-to-grid-matching more permissive (might help when your plate is at a slight angle).|float > 2|3
imageThreshold|By default the intensity threshold to distinguish colonies from background is determined by the Otsu method. The determined value will be multiplied by image_threshold to give the final threshold.|float > 0|1
sizeThreshold|Detected putative colonies will be filtered by size and small components (usually image noise) will be excluded. The default threshold is the image width divided by 32 and it is therefore independent of scanning resolution. This default is then multiplied by size_threshold to give the final threshold.|float > 0|1
negateQ|Should the image be colour inverted before processing? Images acquired with transmission scanning will generally require this. This option does not apply to cfuq_john |Boolean|True
hardImageThresholdQ|Should a hard (fixed) intensity threshold should be used instead of Otsu thresholding? If this is set to True, imageThreshold will be ignored|Boolean|False
hardImageThreshold|The intensity threshold used if hardImageThresholdQ is True| 0 < float < 1|0.5
hardSizeThresholdQ|Should a hard (fixed) size threshold should be used instead of scaling pixel counts with image size? If this is set to True, sizeThreshold will be ignored|Boolean|False
hardSizeThreshold|The size threshold (number of pixels) used if hardSizeThresholdQ is True| int > 0|50
onlyNearestQ|Only use the closest putative colonie (image component) for each grid position|Boolean|True
useWorklistQ|Use a worklist of image paths instead instead of analysing all images in the current directory. This is usefuls if your images are spread out over several (sub-)directories. If this option is set True, a file called "worklist.txt", containing one relative or absolute image path per line, must exist in the directory from which spotsizer2 is called.|Boolean|False
