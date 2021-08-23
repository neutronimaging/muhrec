# Center estimation

## Description

## Example
```python
import imgalg
# cproj is a 3D image containing all projections of the scan
img0   = cproj[0,:,:]
img180 = cproj[312,:,:] # This is the projection at the opposite side of the 0. Which projection you select depends on the length of the scan.  

ce = imgalg.TomoCenter()

cest = ce.estimate(img0,img180,imgalg.centerLeastSquare,True)

print('Center: {0:0.2f}, Tilt angle: {1:0.02f}, Pivot point: {2:0.02f}'.format(cest[0],cest[1],cest[2]))
```

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
|float fraction|The fraction value, should be in the interval 0-1. The default is 0.9|

### ```estimate(img0deg,img180deg,esttype,bTilt)```
#### Interface
|Arguments| Description|
|-|-|
|2D Array x0| Image at 0 degrees|
|2D Array x180| Image at 180 degress |
|ImagingAlgorithms::TomoCenter::eEstimator est | Selects the estimator type for the fit|
|bool bTilt| Selects if tilt should be fitted |

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
| Arguments| Description |
|-|-|
| int y | The vertical position to the get the center|

### ```R2()```
Returns R2 for the fit.

#### Interface
The function doesn't take any parameters

#### Returns
The function returns the R2 value
