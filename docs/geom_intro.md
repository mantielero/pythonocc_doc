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


## Reading a STEP file
For example:

```python
from OCC.STEPControl import STEPControl_Reader
step_reader = STEPControl_Reader()
step_reader.ReadFile('./mystep.stp')
step_reader.TransferRoot()
myshape = step_reader.Shape()
```

Then we can traverse the file searching elements inside. For instance, if we are looking for solids:

```python
from OCC.TopExp import TopExp_Explorer
from OCC.TopAbs import TopAbs_SOLID

topExp = TopExp_Explorer()
topExp.Init(intake_shape, TopAbs_SOLID)
```

Now we can iterate over the explorer:

```python
>>> from OCC.TopTools import TopTools_ListOfShape
>>> seq = []
>>> hashes = []
>>> occ_seq = TopTools_ListOfShape()
>>> topExp.More()
True
>>> item = topExp.Current()
>>> item
class<'TopoDS_Shape'; Type:Solid; id:916570656>
>>> dir(item)
['Checked', 'Closed', 'Complement', 'Complemented', 'Compose', 'Composed', 'Convex', 'EmptyCopied', 'EmptyCopy', 'Free', 'HashCode', 'Infinite', 'IsEqual', 'IsNotEqual', 'IsNull', 'IsPartner', 'IsSame', 'Located', 'Location', 'Locked', 'Modified', 'Move', 'Moved', 'Nullify', 'Orientable', 'Orientation', 'Oriented', 'Reverse', 'Reversed', 'ShapeType', 'TShape', '__class__', '__delattr__', '__dict__', '__dir__', '__doc__', '__eq__', '__eq_wrapper__', '__format__', '__ge__', '__getattribute__', '__getstate__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__le__', '__lt__', '__module__', '__ne__', '__ne_wrapper__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__setstate__', '__sizeof__', '__str__', '__subclasshook__', '__swig_destroy__', '__weakref__', 'this', 'thisown']
>>> item.__hash__()
916570656
```

The hash can be added into the python list, while the shape should be added into `occ_seq = TopTools_ListOfShape()`:

```python
hashes.append(item.__hash__())
occ_seq.Append(current_item)
```

Then we go to the following matching shape using:
```
topExp.Next()
```

So we use:

- `topExp.Current()`: to get the current shape
- `topExp.More()`: in order to know if there are more shapes.
- `topExp.Next()`: in order to go to the following shape.

The convenient class `Topo` is defined in [core_topology_traverse.py](https://github.com/tpaviot/pythonocc-core/blob/0.18.1/examples/core_topology_traverse.rst). It is used in the example [core_geometry_face_recognition_from_stepfile.py](https://github.com/tpaviot/pythonocc-core/blob/0.18.1/examples/core_geometry_face_recognition_from_stepfile.rst).

## Viewing in a web page
To view a STEP file in the browser:

```python
#!/usr/bin/env python
from OCC.STEPControl import STEPControl_Reader
from OCC.Display.WebGl import x3dom_renderer
from OCC.BRep import BRep_Builder
from OCC.TopoDS import TopoDS_Shape
from OCC.BRepTools import breptools_Read

# loads step
step_reader = STEPControl_Reader()
step_reader.ReadFile('mystep.stp')
step_reader.TransferRoot()
myshape = step_reader.Shape()

my_renderer = x3dom_renderer.X3DomRenderer()
my_renderer.DisplayShape(myshape)
my_renderer.render()
```

In order to view a BREP file:

```python
# loads brep shape
cylinder_head = TopoDS_Shape()
builder = BRep_Builder()
breptools_Read(cylinder_head, './models/cylinder_head.brep', builder)
```

See the examples:

- [core_webgl_x3dom_cylinderhead.py](https://github.com/tpaviot/pythonocc-core/blob/0.18.1/examples/core_webgl_x3dom_cylinderhead.py)
- [core_webgl_x3dom_random_boxes.py](https://github.com/tpaviot/pythonocc-core/blob/0.18.1/examples/core_webgl_x3dom_random_boxes.py): this shows random boxes. This viewer has the advantage of being able to hide/show shapes. This can be done by adding one shape at a time.
- []
- []

https://github.com/tpaviot/pythonocc-core/blob/0.18.1/examples/core_webgl_threejs_random_toruses.py

https://github.com/tpaviot/pythonocc-core/blob/0.18.1/examples/core_webgl_threejs_torus.py

http://www.pythonocc.org/resources/tutorial/gettin-started-with-pyqt-wxpython-and-pythonocc/

## Filtrado
Haremos:
