# Geometry introduction
We can load a number of classes from the Geometry Procesor:

```python
from OCC.gp import gp_Pnt, gp_Vec, gp_Pnt2d, gp_Pln, gp_Dir
```

With those classes we can:
```python
# create points
pnt1 = gp_Pnt(0,0,0)

# create direction
dir1 = gp_Dir(0,0,1)

# create a plane
plan = gp_Pln(gp_Pnt(0,0,0), gp_Dir(0,0,1)) # Z=0 plan / XY plan
```
