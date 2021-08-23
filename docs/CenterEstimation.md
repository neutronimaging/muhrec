# Center estimation

## Description

## Enums
|Enum value| Description|
|-|-|
|centerLeastSquare ||
|centerCorrelation ||
|centerCenterOfGravity||

## TomoCenter API

### Constructor
Creates an instance of the TomoCenter class

#### Interface
The constructor doesn't have any arguments.

### ```setFraction(fraction)```
Set the mid quantile fraction of center estimates to use for the linear fit of the center line.
|Argument| Description|
|-|-|
|fraction|The fraction value, should be in the interval 0-1. The default is 0.9|

### ```estimate(img0deg,img180deg,esttype,bTilt)```
#### Interface
|Arguments| Description|
|x0||
|x180||
|ImagingAlgorithms::TomoCenter::eEstimator est | |
|bool bTilt| |

#### Returns
A tuple containing (center,tilt,pivot)

### ```centers()```

#### Interface
The function doesn't take any arguments
#### Returns
Returns a vector with all centers

### ```tiltParameters()```
Returns the linear fit coefficients for the center line

#### Returns
A tuple with k and m
   
### ```center(y)```
Returns the center at vertical position y

#### Interface
|||
|-|-|
| int y | The vertical position to the get the center|

### ```R2()```
Returns R2 for the fit.

#### Interface
The function doesn't take any parameters

#### Returns
The function returns the R2 value
