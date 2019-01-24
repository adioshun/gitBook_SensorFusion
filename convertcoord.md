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