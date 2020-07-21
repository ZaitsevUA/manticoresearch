# Geo spatial functions

### GEODIST()
`GEODIST(lat1, lon1, lat2, lon2, \[...\])` function computes geosphere distance between two given points specified by their coordinates. Note that by default both latitudes and longitudes must be in **radians** and the result will be in **meters**. You can use arbitrary expression as any of the four coordinates. An optimized path will be selected when one pair of the arguments refers directly to a pair attributes and the other one is constant.

`GEODIST()` also takes an optional 5th argument that lets you easily convert between input and output units, and pick the specific  geodistance formula to use. The complete syntax and a few examples are as follows:

```sql
GEODIST(lat1, lon1, lat2, lon2, { option=value, ... })

GEODIST(40.7643929, -73.9997683, 40.7642578, -73.9994565, {in=degrees, out=feet})

GEODIST(51.50, -0.12, 29.98, 31.13, {in=deg, out=mi}}
```

The known options and their values are:

* `in = {deg | degrees | rad | radians}`, specifies the input units;
* `out = {m | meters | km | kilometers | ft | feet | mi | miles}`, specifies the output units;
* `method = {adaptive | haversine}`, specifies the geodistance calculation method.

The default method is "adaptive". It is well optimized implementation that is both more precise *and* much faster at all times than "haversine".

### GEOPOLY2D()
`GEOPOLY2D(lat1,lon1,lat2,lon2,lat3,lon3...)` produces a polygon to be used with the [CONTAINS()](Functions/Geo_spatial_functions.md#CONTAINS%28%29) function. This function takes into account the Earth's curvature by tessellating the polygon into smaller ones, and should be used for larger areas. For small areas [POLY2D()](Functions/Geo_spatial_functions.md#POLY2D%28%29) function can be used instead. The function expects coordinates to be pairs of latitude/longitude coordinates in degrees, if radians are used it will give same result as `POLY2D()`.    

### POLY2D()
`POLY2D(x1,y1,x2,y2,x3,y3...)` produces a polygon to be used with the [CONTAINS()](Functions/Geo_spatial_functions.md#CONTAINS%28%29) function. This polygon assumes a flat Earth, so it should not be too large; for large areas the [GEOPOLY2D()](Functions/Geo_spatial_functions.md#GEOPOLY2D%28%29) function which takes Earth's curvature in consideration should be used.