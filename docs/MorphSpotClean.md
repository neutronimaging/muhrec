# MorphSpotClean
The reconstructor class creates a back-projector and allows you to configure the reconstruction.

## Enums 

### Detection method

The ```eMorphDetectionMethod``` enum is used to select the spot detection algorithm.

| enum value | Description |
|-|-|
|MorphDetectDarkSpots| New algorithm to detect dark outliers in the image|
|MorphBrightSpots| New algorithm to detect bright outliers in the image|
|MorphDetectAllSpots| Combining DetectDarkSpot and DetectBrightSpots|
|MorphDetectHoles| Original algorithms to the detect dark outliers |
|MorphDetectPeaks|Original algorithms to the detect dark outliers |
|MorphDetectBoth| Combining DetectHoles and DetectPeaks|


### Correction method
The ```eCorrectionMethod``` enum is used to select how the outliers are corrected in the image.
 
| enum value | Description |
|-|-|
|MorphCleanReplace| Standard method that uses the detection image value as replacement for the outlier (default value)|
|MorphCleanFill| Experimental -  don't use|

## The MorphSpotClean API

### ```MorphSpotClean()```
Creates a reconstructor object and binds a backprojector algorithm.

#### Interface
MorphSpotClean constructor doesn't take any arguments.

### ```setConnectivity(conn)```
Sets the mophological connectivity for thhe operations. Default value is 8-connectivity.
#### Interface

|Argument| Description|
|-|-|
|conn| Sets the mophological connectivity (kipl::morphology::conn8)|


### ```setCleanMethod(detectionMethod,cleanMethod)```

### ```cleanMethod()```
Returns the current clean method.

### ```detectionMethod```
Returns the current detection method.

### ```setLimits(applyClamp,vmin,vmax,maxarea)```
Set limit on the image values and sizes of blobs

### ```clampLimits()```
Returns a vector containing the data clamping lower and upper limits.

### ```clampActive()```
Returns true if data clamping is active.")

### ```maxArea()```
Returns the max area of detected spots to be accepted for cleaning.

### ```cleanInfNan()```
Makes a check and replaces possible Inf and Nan values in the image before cleaning.

### ```setEdgeConditioning()```
Sets the length of the median filter used to precondition the image boundaries.

#### Interface

|Argument| Description|
|-|-|
|length| Length of the edge smoothing filter|

### ```edgeConditionLength()```
Returns the lenght of the edge conditioning filter.

### ```detectionImage(x,remove_bias)```

#### Interface

|Argument| Description|
|-|-|
|x|input image (2D only)| 
|remove_bias| Switch to tell if the returned image is the full image with filled outliers of if the trend is subtracted|


### ```process(img,th,sigma)```
Cleans spots from the image in place using th as threshold and sigma as mixing width. The function shuld be able to take either double or single precision images and parameters

#### Interface

|Argument| Description|
|-|-|
|img| An 2D or 3D image. If a 3D image is provided, slices will be processed along axis=0|
|th| vector containing the threshold values|
|sigma| vector containing the width of the mixing band|
