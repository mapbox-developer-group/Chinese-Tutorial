---
title: Extend Mapbox Boundaries
description: Extend the Mapbox Boundaries tileset.
level: 3
topics:
- data
language:
- No code
thumbnail: extendEnterpriseBoundaries
prereq: Familiarity with front-end development, command line tools, and GIS. Access to Mapbox Boundaries.
prependJs:
  - "import Note from '@mapbox/dr-ui/note';"
  - "import BookImage from '@mapbox/dr-ui/book-image';"
contentType: tutorial
---

{{
  <Note title='Access to Mapbox Boundaries' imageComponent={<BookImage />}>
    <p>Access to the Boundaries tilesets are controlled by Mapbox account access token. If you do not have access on your account, <a href='https://www.mapbox.com/contact/'>contact a Mapbox sales representative</a> to request access to Boundaries tilesets.</p>
  </Note>
}}

In some cases, Mapbox Boundaries may cover most of your needs, but you may need a few specific school districts, neighborhoods, or sub-market boundaries for your customers. You can extend Mapbox Boundaries with any custom data and deliver the same frontend, API-driven services for data visualization, analysis, and geofencing applications around the world.

This guide walks through how to format, tile, and host data to work in your application alongside Mapbox Boundaries.

![final map in Mapbox GL JS](/help/img/data/extend-ent-boundaries-final-product.gif)

## Getting started

Here are a few resources you'll need throughout this tutorial:

- **Access to Mapbox Boundaries**. Mapbox Boundaries are available as a part of an Enterprise plan. If you do not have an Enterprise plan or if you do have an Enterprise plan and would like to add access to Mapbox Boundaries, <a href='https://www.mapbox.com/contact/'>contact a Mapbox sales representative</a> to request access. Access to the Boundaries tilesets are controlled by Mapbox account access token.
- **Data**. In this tutorial, you'll learn how to add sub-county data from US Census to Mapbox Boundaries. Use the [US Census FTP site](ftp://ftp2.census.gov/geo/tiger/TIGER2016/COUSUB/) to download all files in the US Census Subcounty directory.
  - _Note: The process outlined in this guide requires that your custom data:_
    - _Uses polygon or multi-polygon geometries._
    - _Has metadata for each polygon feature denoting an identifier._
- **QGIS**. QGIS is an open source GIS application. You can download it from [http://www.qgis.org/](http://www.qgis.org/en/site/). You should be somewhat familiar with the QGIS interface before starting this tutorial.
- **Tippecanoe**. [Tippecanoe](https://github.com/mapbox/tippecanoe#tippecanoe) is a command line tool for creating Mapbox tilesets.
- **Mapbox CLI**. You'll use the [Mapbox CLI](https://github.com/mapbox/mapbox-cli-py/) (command line interface) to upload the tileset you create with Tippecanoe to your Mapbox account.


## Format Data

You'll do two things to format the data before creating Mapbox tilesets:

1. **Concatenate the data** into one GeoJSON format file per administrative level.
1. **Generate a unique identifier** as a property value named id for each feature that matches the Mapbox Boundaries format.

![screenshot of a map of the United States in QGIS](/help/img/data/extend-ent-boundaries-map.png)

### Concatenate the data

In QGIS, open all the US sub-county shapes. Then, you'll need to:

1. Merge the subcounty Shapefiles together into one master Shapefile.
1. Create a unique identifier named `id`.
1. Project the data to `EPSG:4326 (WGS84)`.
1. Export the polygon data with needed properties to GeoJSON file.
1. Export the point data with needed properties to a GeoJSON file.

### Generate a unique identifier

Next, you'll generate a unique identifier for each feature. The globally unique identifier should have the format:

- The leftmost 2 characters are the ID of the admin level 0 parent polygon &mdash; this is the 2-digit ISO country code.
- The third character from the left is `A`, `P`, or `S` representing admin, postal, or stats.
- The fourth character from the left is a number representing the admin or postal level.
- The remaining characters are the ID correspond to the individual admin or postal feature.
- To complete steps 1 and 2 on data format, either use your own data processing pipeline (such as PostGIS, SQLServer, Oracle Spatial) or a GIS tool such as ArcGIS or the open source tool QGIS.

The unique identifier will take the form `[CC-AL-D*]` where:

- `CC` is the two digit country code.
- `AL` is the two digit representation of admin-level (A for administrative, P for postal, S for statistical, and L for the level 0-5).
- `D*` is the administrative code for the feature.

In this example, to create the unique identifier in QGIS, open the merged layer properties and create a custom expression to add a new string field.

<img alt='screenshot of the add field window in QGIS' src='/help/img/data/extend-ent-boundaries-add-field.png' class='wmax360 mx-auto block'>

Sub counties should fall to level admin-3 in the Boundaries hierarchy &mdash; one level of detail down from counties at admin-2. Thus the unique ID should be the following formula `USA3` + `{admin code of sub county feature}`:

<img alt='screenshot of where to assign an id in QGIS' src='/help/img/data/extend-ent-boundaries-unique-id.png' class='wmax480 mx-auto block'>

When you are done editing the id, save the layer edits and export the shape file as a 6-coordinate-precision GeoJSON file in coordinate system `WGS84 (EPSG:4326)` named `admin-3-us-poly.geojson`.

Next create a point layer from the `INTERPLONG` and `INTERLAT` columns, which correspond to feature centroids. Export this centroid point layer to a GeoJSON file with coordinate precision 6 in coordinate system `WGS84 (EPSG:4326)` named `admin-3-us-point.geojson`.

{{
  <Note imageComponent={<BookImage />}>
    <p>If you are working with data that does not have pre-calculated centroid points, calculate the centroid using a GIS tool.</p>
  </Note>
}}

## Create tiles

To create tilesets from your custom data, use the command line tool [Tippecanoe](https://github.com/mapbox/tippecanoe#tippecanoe) to transform your GeoJSON features to vector tiles. You'll need to create two source layers and merge them together into a single tileset source:

1. One source layer with a unique name for all polygons with an `id` property.
1. One source layer for with a unique name for centroid points with an `id` property. _Note: you can also encode other data beyond the `id` property, but it will result in bigger tiles and require you to set a higher min zoom for your tileset._

### Create the polygon source layer

Start by creating a polygon source layer. Use the following Tippecanoe command to transform the example files.

Substitute the name of your layer in for the `-l` parameter, and adjust the minimum zoom of the tileset with the `-Z` parameter. Typically admin-2 features will have `-Z2`, admin-3 will have `-Z4`, admin-4 will have `-Z6`, and admin-5 will have `-Z7`.

```bash
tippecanoe -P -f -o admin-3-poly-us.mbtiles -l boundaries_admin_3_us -Z4 -z12 admin-3-us-poly.geojson -y "id"
```

### Create the point source layer

Next, create a point source layer using the following Tippecanoe command. You can adjust the `-Z` value to specify the minimum zoom of the tileset &mdash; this will help keep tile sizes small. Generally, you can pick a higher minimum zoom level the more dense your features are.

```bash
tippecanoe -P -f -o admin-3-point-us.mbtiles -l points_admin_3_us -Z4 -z12 -r0 admin-3-us-point.geojson -y "id"
```

### Create a single tileset

Then, join the two polygon and point layers into one vector tileset using the following command:

```bash
tile-join -f -o admin-3-us.mbtiles admin-3-poly-us.mbtiles admin-3-point-us.mbtiles
```

Upload the tileset to your Mapbox account. Start by installing the [Mapbox CLI](https://github.com/mapbox/mapbox-cli-py/). Adjust the tileset name to use your Mapbox account name and level with a suffix to denote that it is unique from Mapbox Boundaries.

```bash
pip install mapboxcli
export MAPBOX_ACCESS_TOKEN=MY-UPLOAD-SCOPE-TOKEN
mapbox upload "admin-3-us.mbtiles" "MY-ACCOUNT-NAME.enterprise-boundaries-a3-us"
```

{{
  <Note title='Alternative upload process' imageComponent={<BookImage />}>
    <p>Alternatively, you can upload your tileset using <a href='https://www.mapbox.com/studio/tilesets/'>Mapbox Studio</a>.</p>
  </Note>
}}

## Composite tiles

After the tileset has been successfully added to your account, you can use the syntax below to composite Boundaries with custom boundaries in a map [style](/help/glossary/style/). This puts all tile data into one API request, maximizing performance and minimizing API calls. Compositing also improves label placement calculations across tilesets.

```json
"sources": { "composite": { "url": "mapbox://mapbox.enterprise-boundaries-a3-v2,MY-MAPBOX-ACCOUNT.enterprise-boundaries-a3-us", "type": "vector" } }
```

{{
  <Note imageComponent={<BookImage />}>
    <p>Find the complete list of Mapbox Boundaries tilesets in the <a href="https://www.mapbox.com/vector-tiles/enterprise-boundaries-v2">reference documentation</a>.</p>
  </Note>
}}

## Final product

Here is an example style showing how the new US Admin Level 3 data works alongside the base Mapbox Boundaries product.

![final map in Mapbox GL JS](/help/img/data/extend-ent-boundaries-final-product.gif)

## Next steps

Learn more about how you can use Mapbox Boundaries:

- [Point-in-polygon query with Mapbox Boundaries](/help/tutorials/point-in-polygon-query-with-enterprise-boundaries/): Determine what polygons exist at a single point using the Mapbox Tilequery API.
- [Data-joins with Mapbox Boundaries](/help/tutorials/data-joins-with-enterprise-boundaries/): The data-join technique involves inner joins between local data, such as the unemployment rate by US state, to vector tile features, such as admin boundaries in Mapbox Boundaries, using data-driven style notation.
