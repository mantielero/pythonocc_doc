# Geometry introduction
- [tutorial pdf](http://trac.lecad.si/vaje/raw-attachment/wiki/PythonOcc/VisualizationOfGeometryWithUtilisingpythonOCC.pdf)
- [examples](https://github.com/tpaviot/pythonocc-core/tree/0.18.1/examples)

We can load a number of classes from the Geometry Procesor:

```python
from OCC.gp import gp_Pnt, gp_Pln, gp_Dir
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

## 2D geometry
We can sketch in 2d geometry:

```python
from OCC.Display.SimpleGui import init_display
from OCC.gp import gp_Lin2d, gp_Pnt2d, gp_Dir2d
from core_geometry_utils import make_edge2d

display, start_display, add_menu, add_function_to_menu = init_display()

# Creating 2d points
p1 = gp_Pnt2d(2.,3.)
p2 = gp_Pnt2d(2.,5.)
display.DisplayShape( p1 )
display.DisplayShape( p2, update=True )

# Creating a 2d line requires: a point and a direction
d1 = gp_Dir2d(1.,1.)
l1 = gp_Lin2d(p1, d1)
display.DisplayShape(make_edge2d(l1), update=True )
```

To draw a circle, something as follows:

```python
from OCC.gp import gp_Circ2d, gp_Ax22d

# Draws a circle geometry using gp_Ax22d and radius=4
ci1 = gp_Circ2d(gp_Ax22d(), 4)
display.DisplayColoredShape(make_edge2d(ci1), update=True, color="BLUE" )
```

Let's talk about [gp_Ax22d](https://www.opencascade.com/doc/occt-6.9.0/refman/html/classgp___ax22d.html).



```
from OCC.GCE2d import GCE2d_MakeLine, GCE2d_MakeCircle
from OCC.GccAna import GccAna_Lin2dBisec, GccAna_CircLin2dBisec, GccAna_Pnt2dBisec
```


```python
from OCC.gp import gp_Vec
```
## Axis


core_geometry_axis.py



core_geometry_airfoil.py
core_geometry_axis.py
core_geometry_bisector.py
core_geometry_bounding_box.py
core_geometry_bspline.py
core_geometry_curves2d_from_curve.py
core_geometry_curves2d_from_offset.py
core_geometry_face_recognition_from_stepfile.py
core_geometry_faircurve.py
core_geometry_geomplate.py
core_geometry_medial_axis_offset.py
core_geometry_minimal_distance.py
core_geometry_parabola.py
core_geometry_point_from_curve.py
core_geometry_point_from_intersection.py
core_geometry_project_point_on_curve.py
core_geometry_quaternion.py
core_geometry_splinecage.py
core_geometry_surface_from_curves.py
core_geometry_utils.py
