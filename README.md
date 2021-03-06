# Nodiverse

## What is Nodiverse?

Nodiverse is a 3D Universe generator Node.js library.

### Installation

The latest stable version of Nodiverse can be installed via npm:
```
    npm install nodiverse 
```

### Usage

```
    var nodiverse = require('nodiverse'); // library load
    var myverse = nodiverse();            // my universe object creation
    // let's create a place... 
    // let's say, a room in the center of the universe, with a
    // passage towards north and another towards southeast
    myverse.create([0,0,0], myverse.N + myverse.SE);
    // let's get a local copy of that place, maybe to change it
    var myplace = myverse.get([0,0,0]);
    myplace.name = "clearing";
    myplace.description = "This is a clearing.";
    // let's update the universe with this place's changes
    myverse.update(myplace);
    // let's see where to can we go from here (through the passages)
    myverse.get_neighbours(myplace);
    // we can, of course, also destroy a place
    myverse.nuke([0,0,0]);
    // and if we want to update the universe properties themselves:
    myverse.geometry="plane";
    myverse.entrypoint=[0,0,0];
    // finally, it might be useful to be able to see a visual representation
    // of the universe...
    console.log(myverse.asciimap());
    // ...well, maybe you want to see the map of a particular part of the
    // universe:
    console.log(myverse.asciimap([1,1,1]));
```

#### About the coordinates

 * x-axis (coords[0]) is "East to West"
 * y-axis (coords[1]) is "South to North"
 * z-axis (coords[2]) is "Down to Up"

Eg (2D):
```
    N     [0,1,0]
   W+E    [0,0,0] [1,0,0]
    S
```

#### Universe maleability

A Nodiverse should be maleable, but -- for now -- every Nodiverse is a
3-dimensional Euclidean space. While there are no immediate plans to support
n-dimensional universes (meaning: universes with less or more than three
dimensions), there should be support to other 3-dimensional universes. For
instance: supporting a spheric universe would be a very user-friendly way of
representing a planet.

#### Universe consistency

When you have a passage opened to some place that doesn't really exist, it
doesn't really matter: you can't go through no matter if the passage exists or
not. But when you have a passage to some place that exists, then that place
also needs a passage to you, in order to maintain universe consistency. In
other words: if you can go north from here, you can go south from there.

When creating a place, the passages marked on that place are the ones which are
to be maintained. That means that if a place is created next no another one,
weather the newly created place has a passage to its neighbour or not mandates
the final result: passages on neighbours are either created or destroyed to
accomodate it.

### Nodiverse in action

This is being used on:
* TalkerNode - <https://github.com/marado/TalkerNode>

If you want to add to this list, just submit a change!
