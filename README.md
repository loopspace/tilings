# Tilings

This is a TikZ library for working with tilings.
It can be used to define _tiles_ which can be placed alongside each
other to produce a _tiling_.

To use this library, load the TikZ package and then use:

```
\usetikzlibrary{tilings}
```

There are also libraries with pre-defined tiles:

* **Penrose tiles**

  ```
  \usetikzlibrary{tilings.penrose}
  ```
  
  This defines sets of Penrose tiles: kite/dart, the two rhombi, and
  the pentagonal tile sets.
  
* **polykite tiles**

  ```
  \usetikzlibrary{tilings.polykite}
  ```
  
  These are the tiles defined in [the aperiodic
  monotile](https://arxiv.org/abs/2303.10798).
  
Each of these loads the main `tilings` library and then defines
certain sets of tiles.

## Defining tiles

The command to define a tile is:

```
\DefineTile{<name>}{<edges>}{<vertices>}
```

* The name is its label.
* The edges is a list of labels for each edge in terms of its matching
  pair.  An edge labelled `a` will match against an edge labelled `A`.
  Edges labelled with numbers will match against themselves.  Edges
  `a` to `e` (and `A` to `E`) and `1`, `2`, `3` are available by
  default, more edges can be defined if needed.
* The vertices is a list of vertices of the tile in the same order as
  the edges.  The expectation is that these will go in the same
  direction around each tile (though this can be swapped when the tile
  is placed).  The first edge goes between the first two vertices
  and so on.  Each vertex is specified by giving its coordinates in
  the form `{ x, y}` and these will be put through the LaTeX3 floating
  point parser.

When a tile has been defined it must still be _baked_.  This is
because there is the facility to replace the default straight edges by
more complicated paths.  To _bake_ a tile is simple:

```
\BakeTile{<name>}
```

## Using tiles

The simplest way to use the tiles is with the `pic` syntax of TikZ.
When a tile is defined then it in turn defines a `pic` of the same
name.  The tiles can be positioned alongside existing tiles using a
key:

```
align with=<tile> [back] along <edge> [using <index>]
```

* `<tile>` is the name of an existing tile.
* `<edge>` is the label of an edge of that tile; if there are multiple
  edges with the same label then they are further modified with an
  index, so the first listed edge of type `a` is `a1` and so on (but
  if there is only one of a type it doesn't get an index).
* `using <index>` is for if the tile to be placed has multiple edges
  with the placing label; this is just the _index_ of the edge.
* `back` this modifier reverses the alignment so that it matches
  against the edge in the "wrong" direction; this is useful if the
  previously placed tile was flipped.

As hinted above, a tile can be "flipped" using the key `flip tile`.

Various styles are used to render the tiles:

* `<name>` when used on the `pic` command (rather than directly as the
  pic type) this installs the `<name>` as the pic type and tries the
  style `every tile pic`.
* A tile is clipped against itself, and the clipping path tries the
  styles `every tile clip` and `every <name> clip`.
* The tile itself is rendered with `every tile`, `every <name>`, and
  the `pic actions`.



