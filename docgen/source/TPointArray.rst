
TPointArray
=============
TPointArray related methods

TPointArray.Mean
~~~~~~~~~~~~~~~~~~~
.. code-block:: pascal

    function TPointArray.Mean(): TPoint; constref;

Wraps Simba's TPAMiddle

TPointArray.MeanEx
~~~~~~~~~~~~~~~~~~~
.. code-block:: pascal

    function TPointArray.MeanEx(): Vector2; constref;

Middle as a Vector.

TPointArray.Sort
~~~~~~~~~~~~~~~~~~~
.. code-block:: pascal

    procedure TPointArray.Sort(From:TPoint=[0,0]);

Wraps Simba's `SortTPAFrom`

TPointArray.Sorted
~~~~~~~~~~~~~~~~~~~
.. code-block:: pascal

    function TPointArray.Sorted(From:TPoint=[0,0]): TPointArray;

Wraps Simba's `SortTPAFrom`, produces a sorted copy.

TPointArray.SortByX
~~~~~~~~~~~~~~~~~~~
.. code-block:: pascal

    procedure TPointArray.SortByX(LowToHi:Boolean=True);

Wraps Simba's `SortTPAByX`

TPointArray.SortByY
~~~~~~~~~~~~~~~~~~~
.. code-block:: pascal

    procedure TPointArray.SortByY(LowToHi:Boolean=True);

Wraps Simba's `SortTPAByY`

TPointArray.SortByRow
~~~~~~~~~~~~~~~~~~~~~
.. code-block:: pascal

    procedure TPointArray.SortByRow(reverse:Boolean=False);

Sorts a given TPointArray TPA row-by-row, starting from the smallest Y coordinate to the largest Y coordinate, and for every row from the smallest X coordinate to the largest X coordinate.

TPointArray.SortByColumn
~~~~~~~~~~~~~~~~~~~~~~~~
.. code-block:: pascal

    procedure TPointArray.SortByColumn(reverse:Boolean=False);

much like SortByRow, but the order of the column comes first

TPointArray.SortFromLine
~~~~~~~~~~~~~~~~~~~~~~~~~
.. code-block:: pascal

    procedure TPointArray.SortFromLine(p,q:TPoint; reverse:Boolean=False);

The name tells the story

TPointArray.Bounds
~~~~~~~~~~~~~~~~~~~
.. code-block:: pascal

    function TPointArray.Bounds(): TBox; constref;

Wraps Simba's GetTPABounds

TPointArray.Density
~~~~~~~~~~~~~~~~~~~
.. code-block:: pascal

    function TPointArray.Density(): Double; constref;

Returns the TPA's density (Length(TPA)/(width*height))

TPointArray.Edges
~~~~~~~~~~~~~~~~~~~
.. code-block:: pascal

    function TPointArray.Edges(): TPointArray; constref;

Filters all points out of the given TPointArray which aren't edge-points. 
Edge-points are points that are on the edge of the TPA, not completely surrounded by other points. 
Same as Simba's `FindTPAEdges`

TPointArray.Cluster
~~~~~~~~~~~~~~~~~~~
.. code-block:: pascal

    function TPointArray.Cluster(dist:Int32): T2DPointArray; constref;
    function TPointArray.Cluster(distX,distY:Int32): T2DPointArray; constref; overload;

Smart wrapper of Simba's `ClusterTPA` and `ClusterTPAEx` (fall backs to `SplitTPA` when it's better suited)

TPointArray.Split
~~~~~~~~~~~~~~~~~~~
.. code-block:: pascal

    function TPointArray.Split(dist:Int32): T2DPointArray; constref;
    function TPointArray.Split(distX,distY:Int32): T2DPointArray; constref; overload;

Wraps Simba's `SplitTPA` and `SplitTPAEx`

TPointArray.ToATPA
~~~~~~~~~~~~~~~~~~~
.. code-block:: pascal

    function TPointArray.ToATPA(WH:Int32): T2DPointArray; constref;
    function TPointArray.ToATPA(W,H:Int32): T2DPointArray; constref; overload;

Wraps Simba's `TPAToATPA` and `TPAToATPAEx`

TPointArray.Offset
~~~~~~~~~~~~~~~~~~~
.. code-block:: pascal

    procedure TPointArray.Offset(off: TPoint);

Wraps Simba's `OffsetTPA`

TPointArray.OffsetFunc
~~~~~~~~~~~~~~~~~~~~~~
.. code-block:: pascal

    function TPointArray.OffsetFunc(off: TPoint): TPointArray;

Wraps Simba's `OffsetTPA`, but offsets a copy, and returns it.

TPointArray.Invert
~~~~~~~~~~~~~~~~~~~
.. code-block:: pascal

    function TPointArray.Invert(Area:TBox=[0,0,-1,-1]): TPointArray; constref;

Inverts the shape based on the area covered, alternatively the given area.
Same as `ReturnPointsNotInTPA` in Simba.

TPointArray.FilterBox
~~~~~~~~~~~~~~~~~~~~~
.. code-block:: pascal

    function TPointArray.FilterBox(Box: TBox): TPointArray; constref;

Returns a filtered version of the TPA.
Same as Simba's `FilterPointsBox`

TPointArray.FilterBox
~~~~~~~~~~~~~~~~~~~~~
.. code-block:: pascal

    function TPointArray.FilterDist(MinDist,MaxDist: Double; Mx,My: Int32): TPointArray; constref;

Returns a filtered version of the TPA.
Same as Simba's `FilterPointsDist`

TPointArray.FilterDuplicates
~~~~~~~~~~~~~~~~~~~~~~~~~~~~
.. code-block:: pascal

    function TPointArray.FilterDuplicates(): TPointArray;

Returns a copy where all duplicate points are removed.

TPointArray.ClearDuplicates
~~~~~~~~~~~~~~~~~~~~~~~~~~~
.. code-block:: pascal

    procedure TPointArray.ClearDuplicates();

Removes all the duplicate points from self.

TPointArray.Rotate
~~~~~~~~~~~~~~~~~~
.. code-block:: pascal

    function TPointArray.Rotate(AngleRad, MidX, MidY: Double): TPointArray;

Returns a copy where all points are rotated around MidX, MidY.
Same as Simba's `RotatePoints`.

TPointArray.SplitRows
~~~~~~~~~~~~~~~~~~~~~
.. code-block:: pascal

    function TPointArray.SplitRows(dist:Int32): T2DPointArray; constref;

Splits a TPA `Arr` into TPAs of each row, it then proceeds to further split the rows
in to separate TPAs when the given distance ``dist`` is less than the distance between the points
Same output as `SplitTPAEx(TPA,dist,0)`, but generally faster.

.. note:: by slacky

Example:

.. code-block:: pascal

    ATPA := TPA.SplitRows(5);

TPointArray.Connect
~~~~~~~~~~~~~~~~~~~
.. code-block:: pascal

    function TPointArray.Connect(): TPointArray; constref;

Fills a line between all the points (by their order), can be used to get the edges
around a polygon

.. note:: by slacky

Example:

.. code-block:: pascal
    
    edges := TPA.ConvexHull().Connect();

TPointArray.ConvexHull
~~~~~~~~~~~~~~~~~~~~~~
.. code-block:: pascal

     function TPointArray.ConvexHull(): TPointArray; constref;

Computes the convex hull around the given TPA. Imagine placing a rubber band around the
points, the points which strech the band are the points returned by this function.

See: http://en.wikipedia.org/wiki/Convex_hull for more information.

.. note:: by slacky

Example:

.. code-block:: pascal

    Smart.Image.DrawTPA(TPA.ConvexHull());

TPointArray.MinAreaRect
~~~~~~~~~~~~~~~~~~~~~~~
.. code-block:: pascal

    function TPointArray.MinAreaRect(): TRectangle;

Computes the minimum bounding box (defined by area) around the given shape.
Four points (which are in order) are always returned.

See: http://en.wikipedia.org/wiki/Minimum_bounding_box for more information.

.. note:: by slacky

Example:

.. code-block:: pascal

    WriteLn('The four box corners are: ', TPA.MinAreaRect());

TPointArray.MinAreaCircle
~~~~~~~~~~~~~~~~~~~~~~~~~
.. code-block:: pascal

    function TPointArray.MinAreaCircle(): TCircle;

Computes the minimum bounding circle around the given shape.

See: https://en.wikipedia.org/wiki/Smallest-circle_problem for more information.

Implementation is a mixture of a few implementations I've seen.

ExpandPolygon
~~~~~~~~~~~~~~

.. code-block:: pascal

    function ExpandPolygon(Poly:TPointArray; inc:Int32): TPointArray;

A method for increasing the size of any convex polygon.

.. note:: by slacky
