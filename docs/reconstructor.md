# Reconstructor
The reconstructor class creates a back-projector and allows you to configure the reconstruction.

## Enums 

### Backprojector selector

The ```eBackprojectors``` enum is used to select the back projection algorithm for the reconstructor.

| enum value | Description |
|-|-|
|bpMultiProj| Create a single threaded backprojector |
|bpMultiProjParallel| Create a multi-threaded backprojector (This doesn't work on MacOS)|
|bpNearestNeighbor| Create a nearest neighbor backprojector. It can be used for quicker reconstructions, but the quality suffers.|

## The Reconstructor API

### ```Reconstructor(eBackprojectors)```
Creates a reconstructor object and binds a backprojector algorithm.

#### Interface
| Input argument | Description |
|-|-|
|eBackprojectors| Selects backprojector algorithm |

### ```name()```
Returns the name of the backprojector algortihm.

### ```configure(dict args)```
Configures the reconstructor object from a dictionary with parameters.

#### Interface
| Input argument | Description |
|-|-|
|args | A dictionary with arguments to control the reconstruction |

#### List of arguments
| Argument | Description | Data type|
|-|-|-|
| center| The position of the acquisition axis (center of rotation)| float |
| tiltangle| Correction angle to adjust tilted acquisition axis (deg)| float |
| tiltpivot| Vertical offset of the rotation point to adjust tilted acquisition axis (deg)| float |
| usetilt  | Switch to use the tilt correction | bool |
| roi | Region of interest in projection space (this parameter is probably not used)| int, list[4] |
| direction | Direction of the acquisition | enum |
| resolution | Pixel size in of the projections | float |
| usematrixroi | Switch to activate cropped reconstruction | bool |
| matrixroi | Region of interest to crop the reconstructed slice | int, list[4]|
| rotate | Rotation angle of the reconstructed object| float |

### ```process(projections, dict args)```
Starts the reconstruction of a set of projections

#### Interface
| Input argument | Description |
|-|-|
|projections| a numpy array with the dimensions nProj x size V x size U.|
|args | A dictionary with arguments to control the reconstruction |

#### List of arguments
| Argument | Description | Data type|
|-|-|-|
| angles| A list with acquisition angles in degrees. The number of angles must match the number of projections| float[nProj] |
| weights| A list of weights for the projections. The basic weight is 1/nProj, but you can also provide golden ratio weighting | float[nProj] |
