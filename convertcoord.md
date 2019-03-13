|![](https://www.mathsisfun.com/images/coordinates-triangle.gif)|![](https://keisan.casio.com/keisan/lib/real/system/2006/1223527679/PolarCartesian.gif)
|-|-|

https://stackoverflow.com/questions/20924085/python-conversion-between-coordinates

https://www.mathsisfun.com/polar-cartesian-coordinates.html

[online tool](https://keisan.casio.com/exec/system/1223527679)

```python

import math

def rect(r, theta):
    """theta in degrees

    returns tuple; (float, float); (x,y)
    """
    x = r * math.cos(theta) #math.cos(math.radians(theta))
    y = r * math.sin(theta) #math.sin(math.radians(theta))
    return x,y

def polar(x, y):
    """returns r, theta(degrees)
    """
    r = (x ** 2 + y ** 2) ** .5
    if y == 0:
        theta = 180 if x < 0 else 0
    elif x == 0:
        theta = 90 if y > 0 else 270
    else:
        theta = math.degrees(math.atan(float(y) / x))
    return r, theta

```


[Converting Cartesian Coordinates to Polar](https://brilliant.org/wiki/convert-cartesian-coordinates-to-polar/)


---

```python
import numpy as np
from math import sin, cos, sqrt

def cartesian_to_polar(x, y, vx, vy, THRESH = 0.0001):
  """   
  Converts 2d cartesian position and velocity coordinates to polar coordinates

  Args:
    x, y, vx, vy : floats - position and velocity components in cartesian respectively 
    THRESH : float - minimum value of rho to return non-zero values
  
  Returns: 
    rho, drho : floats - radius and velocity magnitude respectively
    phi : float - angle in radians
  """  

  rho = sqrt(x * x + y * y)
  phi = np.arctan2(y, x)
  
  
  if rho < THRESH:
    print("WARNING: in cartesian_to_polar(): d_squared < THRESH")
    rho, phi, drho = 0, 0, 0
  else:
    drho = (x * vx + y * vy) / rho
    
  return rho, phi, drho

def polar_to_cartesian(rho, phi, drho):
  """
  Converts 2D polar coordinates into cartesian coordinates

  Args:
    rho. drho : floats - radius magnitude and velocity magnitudes respectively
    phi : float - angle in radians

  Returns:
    x, y, vx, vy : floats - position and velocity components in cartesian respectively
  """
 
  x, y = rho * cos(phi), rho * sin(phi)
  vx, vy = drho * cos(phi) , drho * sin(phi)

  return x, y, vx, vy
```