## Basic usage

````
$ gdal2tiles.py -l -p raster -z 0-5 -w none <image> <tilesdir>
````

Check [test/createtiles.sh](test/createtiles.sh) for usage.

If the `-z` option is omitted then the tool considers the min. zoom level otherwise note...

**Note:** The min zoom level for tile generation must be greater or
equal to `log2(max(width, height)/tilesize)`

Assuming an image with 2000x3000 pixels:

````
# take the larger dimension -> here height = 3000px
$ echo "l(3000/256)/l(2)" | bc -l
# 3.55 --> min zoomlevel for tile generation is 4
# means: `gdal2tiles.py -l -p raster -z 0-2 ...`
#                                          \__ is not allowed
# correct usage
$ gdal2tiles -l -p raster -z 0-4 ...
````
