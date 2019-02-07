# Format convertion
## Introduction
STL and BREP writers can only deal with 1 shape (e.g. 1 box), so if you have many shapes, you have to fuse them so that they can go into a single STL or BREP file

IGES and STEP writers can deal with multiple shapes (e.g. 1 box + 1 cylinder + 1 freeform shape)
## STEP to X3D
For example:

```python
# Python script simplified from the example script
# core_load_step_ap203_to_x3d distributed with pythonOCC
input_file  = 'm12_2.stp'   # input STEP (AP203/AP214 file)
output_file = 'm12_2.x3d'   # output X3D file

from OCC.STEPControl import STEPControl_Reader
from OCC.IFSelect import IFSelect_RetDone, IFSelect_ItemsByEntity
from OCC.Visualization import Tesselator, atNormal
step_reader = STEPControl_Reader()
status = step_reader.ReadFile( input_file )

if status == IFSelect_RetDone:  # check status
    failsonly = False
    step_reader.PrintCheckLoad(failsonly, IFSelect_ItemsByEntity)
    step_reader.PrintCheckTransfer(failsonly, IFSelect_ItemsByEntity)
    aResShape = step_reader.Shape(1)
else:
    print("Error: can't read file.")
    sys.exit(0)

Tesselator(aResShape).ExportShapeToX3D( output_file )
```

## STP to STL
It is done like:

```python
from OCC.STEPControl import STEPControl_Reader
from OCC.StlAPI import StlAPI_Writer

input_file  = 'myshape.stp'   # input STEP (AP203/AP214 file)
output_file = 'myshape.stl'   # output X3D file


step_reader = STEPControl_Reader()
step_reader.ReadFile( input_file )
step_reader.TransferRoot()
myshape = step_reader.Shape()
print("File readed")

# Export to STL
stl_writer = StlAPI_Writer()
stl_writer.SetASCIIMode(True)
stl_writer.Write(myshape, output_file)
print("Written")
```

Based on [this](https://pythonocc.wordpress.com/2013/02/26/creating-an-stl-file-from-a-pythonocc-shape/).
