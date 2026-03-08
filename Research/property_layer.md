Property layer :

1.This is used to store the value of each cell and it is attached to a grid 
2.internally grid keeps a dict of these arrays(values) as attributes 
3.Property layers aren’t just “array storage” – they’re the built‑in way Mesa
lets you put environmental data on the grid and then see it in the
visualiser.


properties to note:
1. Dual Storage Pattern
   self.property_layers[name] = array   # Dict (internal registry)
   setattr(self, name, array)           # Attribute (convenient access)
   Why both? Dict for iteration, attribute for clean API.
2. Dynamic Cell Class Creation:
  1.
   self.cell_klass = type(
    "GridCell",                			 # 1. Name: Call it "GridCell"
    (self.cell_klass,),       			 # 2. Parent: Inherit from the original Cell class
    {"property_layers": set(), "__slots__": ()}  # 3. Extras: Add these features
  )

      Each grid gets its own Cell subclass
      Grid A and Grid B are completely separate
      cell.property_layers is unique per grid

  2. Memory Optimization
       "__slots__": ()
       This tells Python: "Don't allow random new attributes on cells. Only use predefined ones." It saves memory when you have thousands of        
       cells.
3. Pickle Registration

copyreg.pickle(self.cell_klass, pickle_gridcell)

┌─────────────────────────────────────────────────┐
│  Main Process (Core 1)                          │              |
│  - Has Cell objects                             │              |
│  - Needs to send cells to other cores           │              |
└─────────────────────────────────────────────────┘
                    │
                    │ Can't send Python objects directly!
                    ▼
┌─────────────────────────────────────────────────┐
│  Worker Process (Core 2)                        │              |
│  - Needs to receive and use Cell objects        │              |
└─────────────────────────────────────────────────┘

Solution:
Pickle cells → bytes (send over)
Unpickle bytes → cells (receive on other core)

Pickel used to:
 Saving to Disk    pickle.dump(grid, file) works
 Network Transfer  Send grid data to another machine

Serialization = Converting a Python object into a stream of bytes (0s and 1s) so it can be saved or sent.
Deserialization = Converting those bytes back into a Python object.

4. Default "empty" Layer:
  this property tracks which cell is empty and which is filled with agents

  "self.create_property_layer("empty", default_value=True, dtype=bool)"


func
create_property_layer 

Args:
name: str,
default_value=0.0,
dtype=float,
read_only: bool = False

this will create a property layer array and attach it to cells

warning:
We cannot directly reassign the grid.name
grid.sugar[5,5] = 3          # good
grid.sugar[:] = 0             # good
grid.sugar = np.zeros((10,10))  # bad – detaches layer, breaks cells


add_property_layer:

Args:
name:str
array:np.array
read_only:bool=false

this will add the existing array as a property layer 
The array shape should be same as the grid dimension  
It will raise error if the Array shape is not same

remove_property_layer:

This will remove the property layer 
Args: 
name

If the name is not in self.property_layers it will thrown an error


Attach property:
This function is used by the add_add_prperty_layer to add the layer

Args:
name:str
array:np.ndarray
read_only:bool=False
 

if the name is in the grid attribute it will throw error

if the name is in the property_layers it will rasie property_layers already exists

if the name exists in the slot it will rasie the error

 getter : returns the value at the coordinate of the current cell
 setter : It will set the value at the coordinate of the current cell
 accessor: If attach_property layer is read only it will just access          
           the getter else getter and setter 
 
