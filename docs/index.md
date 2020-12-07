# Reconstruction of tomography data 
MuhRec is a reconstruction tool for computed tomography. Originally, it was developed as a GUI based application that allows the user to do interactively tune the reconstruction of the projection data. The tool includes a collection of correction algorithms to prepare the data before reconstruction.

# Try MuhRec
## Using as an application with GUI
The easisest way to use MuhRec is to download a prebuilt release of the tool.<br />
<a href="https://github.com/neutronimaging/imagingsuite/releases" style="text-align: center"><img src='figures/muh4_download.svg' width="150"/></a>

## Using in python scripts
MuhRec can also be used from python which allows you to write scripts for the reconstruction process. Using the reconstruction tool in this manner requires that you build the python bindings.

### Compile the python bindings

### API documentation
The python modules for muhrec are described [here](apidoc).

### A basic example
This example requires that yo have compiled the python binding and also have the ```amglib```-module from [the python script repository](https://github.com/neutronimaging/scripts).
```
import numpy as np
import matplotlib.pyplot as plt
import amglib.readers as io
import amglib.imagingutils as amg
import muhrectomo as mt

ob   = io.readImages('ob_{0:04d}.fits',1,5,averageStack=True).mean(axis=0)
dc   = io.readImages('dark_{0:04d}.fits',1,5,averageStack=True).mean(axis=0)
proj = io.readImages('wood_{0:04d}.fits',1,626) # This takes a while

nproj = amg.normalizeImage(img=proj, ob=ob, dc=dc, doseROI=[100,250,200,300])

cproj = nproj[:,50:920,250:850]
plt.imshow(cproj[0])

Nproj = cproj.shape[0]

# Information per projection
args = {"angles"  : np.linspace(0,360,num=Nproj), 
        "weights" : np.ones(Nproj)/Nproj}

# Geometry information
recon.configure({   "center" : 295, 
                    "resolution" : 0.05
                })

recon.process(cproj[:,500:600,:],args) # Reconstruct a part of the slices (32 slices here)

vol = recon.volume() # Retrieve the reconstructed volume

plt.imshow(vol[0])
```
