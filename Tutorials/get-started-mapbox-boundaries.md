---
title: Get started with Mapbox Boundaries
description: Get started with v2 of the Mapbox Boundaries tileset.
category: Tutorials
level: 2
topics:
- data
language:
- No code
thumbnail: getStartedEnterpriseBoundaries
prereq: Familiarity with front-end development and access to Mapbox Boundaries.
prependJs:
  - "import * as constants from '../../constants';"
  - "import Note from '@mapbox/dr-ui/note';"
  - "import BookImage from '@mapbox/dr-ui/book-image';"
  - "import UserAccessToken from '../../components/user-access-token';"
contentType: tutorial
---

{{
  <Note imageComponent={<BookImage />}>
    <p>Access to the Mapbox Boundaries tilesets are controlled by Mapbox account access token. If you do not have access on your account, <a href='https://www.mapbox.com/contact/'>contact a Mapbox sales representative</a> to request access to Boundaries tilesets.</p>
  </Note>
}}

Mapbox Enterprise users can add global administrative, postal, and statistical boundaries to their maps and data visualizations. This guide covers how to use Mapbox Boundaries in a web application and navigate feature lookup tables.

![image of the Mapbox Boundaries tileset in x-ray mode](/help/img/data/enterprise-boundaries-xray.png)

## Getting started

Mapbox Boundaries are available as a part of an Enterprise plan. If you do not have an Enterprise plan or if you do have an Enterprise plan and would like to add access to Mapbox Boundaries, <a href='https://www.mapbox.com/contact/'>contact a Mapbox sales representative</a> to request access. Access to the Boundaries tilesets are controlled by your Mapbox account access token.

## Add to an application

Once you have access to Mapbox Boundaries, you can use them in an application as you would use any other [tileset](/help/glossary/tileset/).

### About Mapbox Boundaries

Below you'll find a few pieces of key information that you'll need to navigate the Mapbox Boundaries tileset.

#### Tileset IDs

Mapbox Boundaries are stored as vector tiles and distributed via the [Mapbox Vector Tiles API](https://docs.mapbox.com/api/maps/#vector-tiles), with a unique tileset for each admin, stats, and postal level. [Tileset IDs](/help/glossary/tileset-id/) for Boundaries tilesets are in the form `mapbox.enterprise-boundaries-{a|p|s}{level}-{version}`. Here are a few examples:

- `mapbox.enterprise-boundaries-a0-v2`: The tileset for admin (`a`) level 0 (`0`) boundaries (which contain countries) in version two (`v2`) of Mapbox Boundaries.
- `mapbox.enterprise-boundaries-p1-v2`: The tileset for postal (`p`) level 1 (`1`) boundaries in version two (`v2`) of Mapbox Boundaries.
- `mapbox.enterprise-boundaries-s3-v2`: The tileset for stats (`s`) level 3 (`3`) boundaries in version two (`v2`) of Mapbox Boundaries.

**Find the complete list of Mapbox Boundaries tilesets and read more about tileset hierarchies in the [reference documentation](https://www.mapbox.com/vector-tiles/enterprise-boundaries-v2/).**

#### Feature IDs

Each [feature](/help/glossary/features/) also has a unique ID that is used to identify a feature polygon. Once Boundaries are added to your account, you will be able to access the reference documentation containing the feature IDs and all identifying metadata.

#### Minimum zoom levels and bounding boxes

- **z_min**: The `z_min` value for each feature indicates the minimum [zoom level](/help/glossary/zoom-extent/) at which a feature is available in a tileset. Use this to set the camera to a minimum zoom level to see the feature.
- **centroid point**: Centroid point features are guaranteed to appear at zoom level `z_min` + 1. Centroid point features can be used to display a marker, symbol, or label at the center of a  Boundaries feature.
  - Access vector tiles containing centroid points for a specific admin, postal, or stat level using the [tileset ID as described above](#tileset-ids) and specifying the [source layer](/help/glossary/source-layer/) `points_{admin|postal|stats}_{level}`. For example, the vector tile source layer `points_postal_4` contains centroid point data for the `mapbox.enterprise-boundaries-p4-v2` tileset.
- **bounds**: Feature bounds are the smallest rectangular envelope that a feature fits into denoted as an array of `[min_long, min_lat, max_long, max_lat]`.


### Example

To use a Mapbox Boundaries tileset in your application, make a request from the Mapbox Vector Tiles API for the relevant tileset. For example, in Mapbox GL JS, load the tileset using the code below:

```js
// Be sure to use an access token from an account
// that has access to Boundaries
mapboxgl.accessToken = '{{ <UserAccessToken /> }}';

var map = new mapboxgl.Map({
  container: 'map',
  style: 'mapbox://styles/mapbox/light-v{{constants.VERSION_LIGHT_STYLE}}',
  center: [-99.9, 41.5],
  zoom: 1
});

map.on('load', function() {

  // Add source for admin-0 Boundaries
  map.addSource('admin-0', {
    type: 'vector',
    url: 'mapbox://mapbox.enterprise-boundaries-a0-v2'
  });
  // Add a layer with boundary lines
  map.addLayer({
    id: 'admin-0-line',
    type: 'line',
    source: 'admin-0',
    'source-layer': 'boundaries_admin_0',
    paint: {
      'line-color': 'red',
      'line-width': ['interpolate', ['linear'], ['zoom'], 0, 2, 20, 10]
    }
  }, 'waterway-label');
  // Add a layer with points
  map.addLayer({
    id: 'admin-0-circle',
    type: 'circle',
    source: 'admin-0',
    'source-layer': 'points_admin_0',
    paint: {
      'circle-color': 'white',
      'circle-stroke-color': 'black',
      'circle-stroke-width': ['interpolate', ['linear'], ['zoom'], 0, 2, 20, 6],
      'circle-radius': ['interpolate', ['linear'], ['zoom'], 0, 2, 20, 20]
    }
  }, 'waterway-label');
});
```

The code above will yield a map with all country boundaries in red with a circle at the center of each country.

![a map with all country boundaries in red with a circle at the center of each country](/help/img/data/enterprise-boundaries-sample.png)

## Feature lookup tables

Each boundary feature is indexed in a lookup table. Lookup tables are designed to be used locally in your application. User data can be joined to Mapbox Boundaries in your application to create a visualization, such as a choropleth map of unemployment by state.

### About feature lookup tables

The Mapbox Boundaries lookup tables include this metadata about each polygon feature:

- **id**: globally unique identifier for the feature.
- **id_int**: an integer-only identifier for a feature that can be used to accomplish data-joins with [Mapbox GL JS's feature state](https://www.mapbox.com/mapbox-gl-js/api/#map#setfeaturestate).
- **type**: either `admin`, `postal` or `stats` to represent the Administrative, Postal or Statistical boundaries types in Mapbox Boundaries.
- **level**: a numeric value between 0 and 5 to represent the level of boundaries within the type.
- **layer**: a shortened concatenation of type and level with feature's administrative (`a`), postal (`p`), or statistical (`s`) hierarchy and level (`0-5`). For example, administrative level 1 would have a level of `a1`.
- **tilesetname**: tileset ID for the tileset containing the feature, see [the reference documentation](https://docs.mapbox.com/vector-tiles/reference/mapbox-boundaries-v2/#tilesets) for more details.
- **worldview**: alternate display of administrative units depending on regional map display requirements (`US`, `CN`, or `IN`).
- **unit_code**: the country-specific identifier for the feature, such as postcode or FIPS code.
- **name**: local feature name.
- **name_ascii**: local feature name converted to ascii characters.
- **names**: any translation or aliases for that boundary.
- **description**: a text qualifier of the level respective to each country's boundary hierarchy. For example, US admin-1 boundaries have a description of `states` while Italian admin-1 boundaries have a description of `regions`.
- **wikidata_id**: the associated [Wikidata ID](https://www.wikidata.org/wiki/Wikidata:Main_Page) for the boundary.
- **source_date**: recency of boundary data.
- **parent_0**: the level-0 parent of a feature which corresponds to the country code.
- **parent_1**: the level-1 parent of a feature, if it exists.
- **parent_2**: the level-2 parent of a feature, if it exists.
- **parent_3**: the level-3 parent of a feature, if it exists.
- **parent_4**: the level-4 parent of a feature, if it exists.
- **z_min**: minimum zoom level at which a polygon feature appears in a tileset.
- **centroid**: The centroid of the boundary in `[long, lat]` format.
- **bounds**: an array of the features bounding box as `[minlong, minlat, maxlong, maxlat]`.
- **polylayername**: name of the source-layer within the tileset containing feature polygon geometry.
- **pointlayername**: name of the source-layer within the tileset containing feature centroid.

Lookup tables are available as JSON.

### Sample workflow

The feature lookup tables are designed to be used alongside the Mapbox Boundaries tilesets. A typical workflow for a business intelligence application is:

1. A user identifies geographic dimensions in a data source, such as state, zip, country, or longitude &amp; latitude.
1. A user makes a query from application data store.
1. Data store joins geographic dimension query results to metadata in the feature lookup table, such as `name`, `unit_code`, or `level`.
1. Data store groups and aggregates results by geographic dimension and sends to the client visualization tool.
1. Generate a Mapbox GL layer from the Mapbox Style Specification to create a visual from query results.
1. The visual style definition works the same across all Mapbox GL products, including Mapbox GL JS on the web, and Mapbox GL Native on iOS, Android, macOS, and Qt.

### Example

Read the [Visualize the USA’s economic recovery with client-side data joins](https://blog.mapbox.com/visualize-the-usas-economic-recovery-with-client-side-data-joins-2aeab23ee9b0) blog post, which illustrates how the steps in the sample workflow can work in your application.

## Next steps

Learn more about how you can use Mapbox Boundaries:

- [Point-in-polygon query with Mapbox Boundaries](/help/tutorials/point-in-polygon-query-with-enterprise-boundaries/): Determine what polygons exist at a single point using the Mapbox Tilequery API.
- [Data-joins with Mapbox Boundaries](/help/tutorials/data-joins-with-enterprise-boundaries/): The data-join technique involves inner joins between local data, such as the unemployment rate by US state, to vector tile features, such as admin boundaries in Mapbox Boundaries, using data-driven style notation.
- [Extend Mapbox Boundaries](/help/tutorials/extend-enterprise-boundaries/): You can extend Mapbox Boundaries with any custom data you need for your application. This could mean adding school district, city, market, or property boundaries to your application &mdash; all with the same performance and API features of the native product.
