---
title: Get started with Mapbox Boundaries v1
description: Get started with v1 of the Mapbox Boundaries tileset.
level: 2
platform: web
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
  - "import { LegacyNote } from '../../components/legacy-note';"
  - "import UserAccessToken from '../../components/user-access-token';"
contentType: tutorial
---

{{
  <LegacyNote
    legacyProduct='Boundaries v1'
    alternativeResource={{
      title: 'Get started with Mapbox Boundaries',
      link: '/help/tutorials/get-started-enterprise-boundaries/'
    }}
  />
}}

{{
  <Note
    title="Access to Mapbox Boundaries"
    imageComponent={<BookImage />}
  >
    <p>Access to the Boundaries tilesets are controlled by Mapbox account access token. If you do not have access on your account, <a href='https://www.mapbox.com/contact/'>contact a Mapbox sales representative</a> to request access to Boundaries tilesets.</p>
  </Note>
}}

Mapbox Enterprise users can add global administrative and postal boundaries to their maps and data visualizations. This guide covers how to use Mapbox Boundaries in a web application, feature lookup tables, data-joins, and the Tilequery API.

![image of the Mapbox Boundaries tileset in x-ray mode](/help/img/data/enterprise-boundaries-xray.png)

## Getting started

Mapbox Boundaries are available as a part of an Enterprise plan. If you do not have an Enterprise plan or if you do have an Enterprise plan and would like to add access to Mapbox Boundaries, <a href='https://www.mapbox.com/contact/'>contact a Mapbox sales representative</a> to request access. Access to the Boundaries tilesets are controlled by your Mapbox account access token.

## Add to an application

Once you have access to Mapbox Boundaries, you can use them in an application as you would use any other [tileset](/help/glossary/tileset/).

### About Mapbox Boundaries

Below you'll find a few pieces of key information that you'll need to navigate the Mapbox Boundaries tileset.

#### Tileset IDs

Mapbox Boundaries are stored as vector tiles and distributed via the [Mapbox Vector Tiles API](https://docs.mapbox.com/api/maps/#vector-tiles), with a unique tileset for each admin and postal level. [Tileset IDs](/help/glossary/tileset-id/) for Boundaries tilesets are in the form `mapbox.enterprise-boundaries-adminOrPostalLevel-version`. For example, admin level 0 boundaries (which contain countries) are at the tileset ID `mapbox.enterprise-boundaries-a0-v1`.

#### Feature IDs

Each [feature](/help/glossary/features/) also has a unique ID that is used to identify a feature polygon. Once Mapbox Boundaries are added to your account, you will be able to access the technical documentation containing the feature IDs and all identifying metadata.

#### Minimum zoom levels and bounding boxes

- **z_min**: The `z_min` value for each feature indicates the minimum [zoom level](/help/glossary/zoom-extent/) at which a feature is available in a tileset. Use this to set the camera to a minimum zoom level to see the feature.
- **centroid point**: Centroid point features are guaranteed to appear at zoom level `z_min` + 1. Centroid point features can be used to display a marker, symbol, or label at the center of a Boundaries feature.
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
    url: 'mapbox://mapbox.enterprise-boundaries-a0-v1'
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

- **id**: globally unique identifier for the feature
- **level**: admin level; admin-0, admin-1....post-3, post-4
- **country_code**: 2-digit ISO code
- **name**: local feature name
- **name_ascii**: local feature name converted to ascii characters
- **admin_code**: feature admin or postal code
- **bounds**: an array of the features bounding box as `[minlong, minlat, maxlong, maxlat]`
- **z_min**: minimum zoom level at which a polygon feature appears in a tileset
- **parent_0**: the level-0 parent of a feature, if it exists
- **parent_1**: the level-1 parent of a feature, if it exists
- **parent_2**: the level-2 parent of a feature, if it exists
- **parent_3**: the level-3 parent of a feature, if it exists
- **parent_4**: the level-4 parent of a feature, if it exists
- **tileset_name**: tileset ID for the tileset containing the feature
- **point_layername**: name of the source-layer within the tileset containing feature centroid
- **poly_layername**: name of the source-layer within the tileset containing feature polygon geometry

Lookup tables are available in two formats: `tsv` and `json`.

### Sample workflow

The feature lookup tables are designed to be used alongside the Boundaries tilesets. A typical workflow for a business intelligence application is:

1. A user identifies geographic dimensions in a data source, such as state, zip, country, or longitude & latitude.
1. A user makes a query from application data store.
1. Data store joins geographic dimension query results to metadata in the feature lookup table, such as name or admin_code.
1. Data store groups and aggregates results by geographic dimension and sends to the client visualization tool.
1. Generate a Mapbox GL layer from the Mapbox Style Specification to create a visual from query results.
1. The visual style definition works the same across all Mapbox GL products, including Mapbox GL JS on the web, and Mapbox GL Native on iOS, Android, macOS, and Qt.

### Example

Read [Visualize the USA’s economic recovery with client-side data joins](https://blog.mapbox.com/visualize-the-usas-economic-recovery-with-client-side-data-joins-2aeab23ee9b0), which illustrates how the steps in the sample workflow can work in your application.

## Data-joins

### About data-joins

The data-join technique are inner joins between local data, such as the unemployment rate by US state, to vector tile features using data-driven style notation.

### Sample workflow

To create a data-join, use the following approach:

- Initialize a Mapbox Style Specification property function object. This will be the data-driven style for a fill layer's color.

```
var color_dds = { "property": "id", "type": "categorical", "default": "rgba(0, 0, 0, 0)", //Set the default color to opacity zero "stops": [] }
```

- Set the stops value of the object to a list of arrays containing the `[id, style value]` of features needed in the visual.

```
color_dds.stops = [['US', 'red'], ['UK', 'green']]
```

- Only features with a matching id in `color_dds.stops` will appear in the visual.
- Set the paint property of the layer to show the visual.

```
map.setPaintProperty('my-layer-name', 'fill-color', color_dds)
```

### Example

Explore this [code example](https://www.mapbox.com/mapbox-gl-js/example/data-join/) to apply the data-join technique to create a choropleth map from user data joined to Boundaries.


## Point-in-polygon query

### About Tilequery

Use the [Mapbox Tilequery API](https://docs.mapbox.com/api/maps/#retrieve-features-from-vector-tiles) to match points to polygons. Example request:

```
https://api.mapbox.com/v4/mapbox.enterprise-boundaries-a0-v1/tilequery/{longitude,latitude}.json?access_token={{ <UserAccessToken /> }}
```

If the point is within a polygon, the Tilequery API response will return a GeoJSON-format body. The id property value of the first feature returned is the ID of the Boundaries feature that contains the queried point.

Since the feature lookup table contains all Mapbox Boundaries parent features, only one API request is required per point to find all matching parent boundaries. For example, you can query the admin-3 boundary of a point in Italy, and use the lookup table to find the parent features at admin-2, admin-1, and admin-0.

### Example

Below is an example API response from a sample query to admin-3 in Italy. The query URL is:

```
https://api.mapbox.com/v4/mapbox.enterprise-boundaries-a3-v1/tilequery/12.87,43.100.json?access_token={{ <UserAccessToken /> }}
```

The `id` returned is the identifier of the Boundaries feature containing the point at admin-3.

```json
{
  "type": "FeatureCollection",
  "features": [{
    "type": "Feature",
    "geometry": {
      "type": "Point",
      "coordinates": [
        12.87,
        43.1
      ]
    },
    "properties": {
      "id": "ITA3054034",
      "tilequery": {
        "distance": 0,
        "layer": "boundaries_admin_3"
      }
    }
  }]
}
```

You can query multiple admin levels in one API call using tile compositing. The query below will return the `admin_ids` at a location for admin-1, admin-2, and admin-3:

```
https://api.mapbox.com/v4/mapbox.enterprise-boundaries-a3-v1,mapbox.enterprise-boundaries-a2-v1,mapbox.enterprise-boundaries-a1-v1/tilequery/12.87,43.100.json?access_token={{ <UserAccessToken /> }}
```

This technique allows for aggregating and visualizing points at any admin level or multiple admin levels, down to individual points, as an API service.

### Example

You can also explore this end to end [example using both the data-join technique and Tilequery API](https://www.mapbox.com/labs/vt-polygons/).

![an end to end example using the data-join technique and Tilequery API](/help/img/data/enterprise-boundaries-choropleth-demo.gif)

## Next steps

You can extend Mapbox Boundaries with any custom data you need for your application. This could mean adding school district, city, market, or property boundaries to your application &mdash; all with the same performance and API features of the native product. For more details, read the [Extend Mapbox Boundaries](/help/tutorials/extend-enterprise-boundaries/) tutorial.
