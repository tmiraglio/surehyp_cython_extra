# Description
Optionnal library for SUREHYP, with callable cython functions for faster processing

# Content
interp3d was modified from https://github.com/jglaser/interp3d/tree/master/interp3d to be able to interpolate 1D vectors and not only scalars.
It is a faster 3D interpolation to replace `scipy.interpolate.RegularGridInterpolator()`

Installation (requires **cython**):

```
python3 setup.py install
```

Usage:

```
from interp3d import interp_3d
import numpy as np

x = np.linspace(0,2.5,100)
y = np.linspace(-1,.5,50)
z = np.linspace(5,25,125)

X,Y,Z = np.meshgrid(x,y,z,indexing='ij')
arr = X+2*Y-3*Z

interp = interp_3d.Interp3D(arr, x,y,z)

from scipy.interpolate import RegularGridInterpolator
interp_si = RegularGridInterpolator((x,y,z),arr)

x0, y0, z0 = (1.1,0.25, 7.5)
print('this class {}'.format(interp((x0,y0,z0))))
print('scipy.interpolate.RegularGridInterpolator() {}'.format(interp_si((x0,y0,z0)), x0+2*y0-3*z0))
print('exact {}'.format(x0+2*y0-3*z0))
```
