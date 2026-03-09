This is my understanding about the raster layer.py in mesa-geo repo

This repo contains;

1.Geobase class:

# This class creates the base layer of the raster layer 

attributes:
_width: int
_height: int
_transform: Affine
_total_bounds: np.ndarray  # [min_x, min_y, max_x, max_y]

This class take the height ,width and then transform it in the real - life coordinates with the help of affine

The methods it includes is 

width:Return the width
height:Return the height
width setter: It will set the width after transform it into the real life coor
height setter : It will set the height after transforming it into the real life coor
total_bounds:It will return the array for [min_x,min_y,max_x,max_y]
total_bound setter:It will set the total bound after transforming it into the real life corr
transform:Return the affine transformation to the raster base layer
Resolution:  Returns the (width, height) of a cell in the units of CRS.
out_of_bound:This will tell you if coordinate is out side the raster layer

_update_transform:This will do the real transformation from cell grid coordinate to real life coordinate

to_crs:This is to overridden by the base class








