# Geometry introduction
[tutorial pdf](http://trac.lecad.si/vaje/raw-attachment/wiki/PythonOcc/VisualizationOfGeometryWithUtilisingpythonOCC.pdf)
[examples](https://github.com/tpaviot/pythonocc-core/tree/0.18.1/examples)

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

## 2D
We can create 2d points


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
