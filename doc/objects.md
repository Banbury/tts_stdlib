# objects
Provides functions to operate on multiple objects at once.

## Usage
Include the file into Global or one of your objects.

```lua
#include !/objects/objects
```

The principle of all functions in this module is, that they loop over all objects
in a table and do something with them.

```lua
objects = Objects.find(getAllObjects(), function(o)
    return o.name=="BlockSquare"
end)
```

This will return a table with all the objects called 'BlockSquare'.

the find method takes a callback function that returns either true or false. It is called for all the objects in the first argument. If the callback returns true the object will be returned. Otherwise it will be skipped.

The condition in the function can be as simple or complex as you want. You could search for all red cubes, or for all objects on the left side of the table, or all objects that are rotated by 90 degrees.

```lua
objects = Objects.getAllHeldByColor("White")
```

This function returns a list of all object held by player 'White'.

```lua
objects = Objects.find(getAllObjects(), function(o)
    return o.name!="BlockSquare"
end)
Objects.execute(objects, function(o) o.highlightOn({1, 1, 0}, 5) end)
```

This code block finds all objects not called 'BlockSquare' and hightlights them in yellow for 5 seconds.

The execute function calls the callback function for every object in the first argument. This can be used to execute complex code on many object.
