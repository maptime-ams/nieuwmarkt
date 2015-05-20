# Maptime AMS #7: Mapping the Nieuwmarkt

It's easy to make beautiful interactive web maps with [Mapbox Studio](https://www.mapbox.com/mapbox-studio/), [Leaflet](http://leafletjs.com/) or [D3.js](https://github.com/mbostock/d3/wiki/Gallery#maps). But if you're designing a map for print, and you want full control over the map design and label placement, there's no way around using GIS software and vector editing software. In the [seventh edition](http://www.meetup.com/Maptime-AMS/events/220184224/) of [Maptime Amsterdam](http://maptime-ams.github.io/), we will use [QGIS](http://www.qgis.org/en/site/) (a Free and Open Source Geographic Information System) and [Inkscape](https://inkscape.org/en/) or [Illustrator](http://www.adobe.com/products/illustrator.html) to design a map of how the Nieuwmarkt looked just before the construction of [Amsterdam's first subway line](http://en.wikipedia.org/wiki/Nieuwmarkt_Riots).

We will use data and information from the following sources:

- Stories told by Ceel Holtkamp during the walking tour,
- Slides from Actiegroep Nieuwmarkt's archive,
- [Amsterdam OpenStreetMap data](https://mapzen.com/metro-extracts/)

And we will design a map showing the construction of the subway:

![](images/nieuwmarkt.jpg)

## OpenStreetMap

Today, we'll use OpenStreetMap data as our main data source. It's easiest to use [Mapzen's Metro Extracts](https://mapzen.com/metro-extracts/) to download OSM data for the Amsterdam metropolitan region. You can download raw OSM XML files and process those yourself, or just download the [OSM2PGSQL Shapefile](https://s3.amazonaws.com/metro-extracts.mapzen.com/amsterdam_netherlands.osm2pgsql-shapefiles.zip). Alternatively, you could use [Overpass Turbo](http://overpass-turbo.eu/) to do a specific OSM query.

Steps:

1. Go to https://mapzen.com/metro-extracts/
2. Download [Amsterdam OSM2PGSQL Shapefile](https://s3.amazonaws.com/metro-extracts.mapzen.com/amsterdam_netherlands.osm2pgsql-shapefiles.zip)

### Data

The OpenStreetMap ZIP-file contains three Shapefiles (each Shapefile consists of a number of files, e.g. `.shp`, `.dbf`, etc.):

- `amsterdam_netherlands.osm-polygon.shp`
- `amsterdam_netherlands.osm-line.shp`
- `amsterdam_netherlands.osm-point.shp`

The properties of an OpenStreetMap feature are defined by its [keys and tags](http://wiki.openstreetmap.org/wiki/Tags). For example, a line with the `railway=rail` tag means the line is a railroad track, a polygon with the tag `building=yes` means the polygon is a building. You can use the values of these properties to style the elements accordingly. Mapbox Studio does this with [CartoCSS](https://www.mapbox.com/guides/cartocss-in-studio/), but you can also do this in QGIS.

Some examples from the OpenStreetMap wiki:

- http://wiki.openstreetmap.org/wiki/Tag:natural%3Dwater
- http://wiki.openstreetmap.org/wiki/Tag:highway%3Dprimary

To get some insight into what keys and tags OpenStreetMap uses, you can use the query tool:

- https://www.openstreetmap.org/query?lat=52.37461&lon=4.90151

![](images/osm-query.png)

Or, if you have an OSM account, you can use the OpenStreetMap editor:

- https://www.openstreetmap.org/edit#map=18/52.37438/4.90243

![](images/osm-edit.png)

For this tutorial, we will make a simple map of the Nieuwmarkt neighbourhood, and we will only use polygon and line data with the following tags:

Polygons:

- Water - [`water`](http://wiki.openstreetmap.org/wiki/Key:water) key
- Buildings - [`building`](http://wiki.openstreetmap.org/wiki/Key:building) key
- natural - [`natural`](http://wiki.openstreetmap.org/wiki/Key:natural) key

Lines:

- Roads - [`highway`](http://wiki.openstreetmap.org/wiki/Key:highway) key
- Railways - [`railway`](http://wiki.openstreetmap.org/wiki/Key:railway) key
- Waterways - [`waterway`](http://wiki.openstreetmap.org/wiki/Key:waterway) key

