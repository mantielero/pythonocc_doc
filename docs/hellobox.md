# HelloBox
[original](https://pythonocc.wordpress.com/2013/02/25/hellobox-the-pythonocc-version-of-helloworld/)

If we type:

```python
from OCC.BRepPrimAPI import BRepPrimAPI_MakeBox
from OCC.Display.SimpleGui import init_display

display, start_display, add_menu, add_function_to_menu = init_display()

my_box = BRepPrimAPI_MakeBox(10.,20.,30.).Shape()

display.DisplayShape(my_box, update=True )
start_display()
```

It will display:
![Hellobox Figure](imgs/hellobox.png =400x)

It needs to be noted that `OCC.BRepPrimAPI` contains Boundary Representations (BRep) primitives such as `BRepPrimAPI_MakeBox` which creates a box based on three lengths.

We add the box to the display and update it.
