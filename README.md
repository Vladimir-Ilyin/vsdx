# vsdx - A python library for processing Visio .vsdx files

#### Note: this is an early release with limited functionality

example code to find a shape with specific text, remove it, and then
save the updated .vsdx file:
```python
from vsdx import VisioFile

filename = 'my_file.vsdx'
# open a visio file
with VisioFile(filename) as vis:
    # get page shapes collection
    shapes = vis.page_objects[0].shapes
    # get shape to remove by its text value
    s = shapes[0].find_shape_by_text('Shape to remove')  # type: VisioFile.Shape
    # remove the shape if found
    if s:
        s.remove()
        # save a new copy
        vis.save_vsdx('shape_removed.vsdx')
```

Please refer to tests/test.py for more usage examples in the form of
pytest tests.

---

###  Change Log
- 0.2.2: Added x & y location setters to Shape, and move(x_delta,
  y_delta) method - both with related tests
- 0.2.3: Updated tests to output files to an /out folder. Added test
  vsdx file with compound shape. Updated Shape text getter/setter
- 0.2.4: Added find_replace(old, new) method to Shape and Page classes
  to recursively replace old with new
- 0.2.5: Add new Shape properties connected_shapes (list of Shape
  objects) and connects (list of Connect objects) properties to allow
  related shapes to be identified (i.e. shapes and connectors) and
  provide information on the relationship, in new Connect object. Also
  new properties of shape begin_x/y, end_x/y, plus height/width
  setters
- v0.2.6: added Page.get_connectors_between() to get zero or many
  connectors between two shapes, by shape id or text
