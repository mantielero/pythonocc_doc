# Format convertion
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
