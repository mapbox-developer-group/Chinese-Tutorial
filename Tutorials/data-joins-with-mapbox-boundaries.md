---
title: Data-joins with Mapbox Boundaries
description: Join data with v2 of the Mapbox Boundaries tileset.
level: 3
topics:
- data
language:
- JavaScript
thumbnail: dataJoinsWithEnterpriseBoundaries
prereq: Familiarity with front-end development and access to Mapbox Boundaries.
prependJs:
  - "import * as constants from '../../constants';"
  - "import Note from '@mapbox/dr-ui/note';"
  - "import BookImage from '@mapbox/dr-ui/book-image';"
  - "import UserAccessToken from '../../components/user-access-token';"
contentType: tutorial
---

{{
<Note
  title="Access to Mapbox Boundaries"
  imageComponent={<BookImage />}
>
  <p>Access to the Boundaries tilesets are controlled by Mapbox account access token. If you do not have access on your account, <a href='https://www.mapbox.com/contact/'>contact a Mapbox sales representative</a> to request access to Boundaries tilesets.</p>
</Note>
}}

Mapbox Enterprise users can add global administrative, postal, and statistical boundaries to their maps and data visualizations. This guide covers how to create a data-join using Mapbox Boundaries with Mapbox GL JS to style a choropleth map.

![final choropleth map using Boundaries, local data, and expressions](/help/img/data/eb-data-join-final.png)

## Getting started

Mapbox Boundaries are available as a part of an Enterprise plan. If you do not have an Enterprise plan or if you do have an Enterprise plan and would like to add access to Mapbox Boundaries, <a href='https://www.mapbox.com/contact/'>contact a Mapbox sales representative</a> to request access. Access to the Boundaries tilesets are controlled by your Mapbox account access token.

## About data-joins

The data-join technique involves inner joins between your custom local data, such as the unemployment rate by US state, to vector tile features, such as state boundaries in the appropriate Mapbox Boundaries tileset, using data-driven style notation.

## Create a data-join with Mapbox Boundaries

Below you'll use Mapbox GL JS, local data, Mapbox Boundaries, feature state, and data-driven styling with expressions to join local data to a vector tile source and style a choropleth map.

### Create a map with Mapbox GL JS

Begin by initializing a map with Mapbox GL JS. Make sure the  access token you are using is from **your account with access to Mapbox Boundaries**.

Here's the starter code for this example:

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset='utf-8' />
    <title>Join local JSON data with Boundaries</title>
    <meta name='viewport' content='initial-scale=1,maximum-scale=1,user-scalable=no' />
    <script src='https://api.tiles.mapbox.com/mapbox-gl-js/{{constants.VERSION_MAPBOXGLJS}}/mapbox-gl.js'></script>
    <link href='https://api.tiles.mapbox.com/mapbox-gl-js/{{constants.VERSION_MAPBOXGLJS}}/mapbox-gl.css' rel='stylesheet' />
    <style>
      body {
        margin: 0;
        padding: 0;
      }

      #map {
        position: absolute;
        top: 0;
        bottom: 0;
        width: 100%;
      }
    </style>
  </head>
  <body>


  <div id='map'>
  </div>
  <script>
    mapboxgl.accessToken = '{{ <UserAccessToken /> }}';

    // Initialize a map
    var map = new mapboxgl.Map({
      container: 'map',
      style: 'mapbox://styles/mapbox/light-v{{constants.VERSION_LIGHT_STYLE}}',
      center: [-99.9, 41.5],
      zoom: 1
    });

    // Local data code from the next step will go here.
  </script>

  </body>
</html>
```

### Local data

In this example, you'll join unemployment data for the US to the admin-1 Boundaries tileset. Here you'll set the array of objects equal to a variable called `localData`. In your own application, you can pull local data into your application how you'd like.

Here's the data used in this example as a JavaScript variable called `localData` that can be directly added to the HTML file's `script` tags alongside the code used to initialize the map:

```js
var localData = [
  { STATE_ID: '01', unemployment: 13.17 },
  { STATE_ID: '02', unemployment: 9.5 },
  { STATE_ID: '04', unemployment: 12.15 },
  { STATE_ID: '05', unemployment: 8.99 },
  { STATE_ID: '06', unemployment: 11.83 },
  { STATE_ID: '08', unemployment: 7.52 },
  { STATE_ID: '09', unemployment: 6.44 },
  { STATE_ID: '10', unemployment: 5.17 },
  { STATE_ID: '12', unemployment: 9.67 },
  { STATE_ID: '13', unemployment: 10.64 },
  { STATE_ID: '15', unemployment: 12.38 },
  { STATE_ID: '16', unemployment: 10.13 },
  { STATE_ID: '17', unemployment: 9.58 },
  { STATE_ID: '18', unemployment: 10.63 },
  { STATE_ID: '19', unemployment: 8.09 },
  { STATE_ID: '20', unemployment: 5.93 },
  { STATE_ID: '21', unemployment: 9.86 },
  { STATE_ID: '22', unemployment: 9.81 },
  { STATE_ID: '23', unemployment: 7.82 },
  { STATE_ID: '24', unemployment: 8.35 },
  { STATE_ID: '25', unemployment: 9.1 },
  { STATE_ID: '26', unemployment: 10.69 },
  { STATE_ID: '27', unemployment: 11.53 },
  { STATE_ID: '28', unemployment: 9.29 },
  { STATE_ID: '29', unemployment: 9.94 },
  { STATE_ID: '30', unemployment: 9.29 },
  { STATE_ID: '31', unemployment: 5.45 },
  { STATE_ID: '32', unemployment: 4.21 },
  { STATE_ID: '33', unemployment: 4.27 },
  { STATE_ID: '34', unemployment: 4.09 },
  { STATE_ID: '35', unemployment: 7.83 },
  { STATE_ID: '36', unemployment: 8.01 },
  { STATE_ID: '37', unemployment: 9.34 },
  { STATE_ID: '38', unemployment: 11.23 },
  { STATE_ID: '39', unemployment: 7.08 },
  { STATE_ID: '40', unemployment: 11.22 },
  { STATE_ID: '41', unemployment: 6.2 },
  { STATE_ID: '42', unemployment: 9.11 },
  { STATE_ID: '44', unemployment: 10.42 },
  { STATE_ID: '45', unemployment: 8.89 },
  { STATE_ID: '46', unemployment: 11.03 },
  { STATE_ID: '47', unemployment: 7.35 },
  { STATE_ID: '48', unemployment: 8.92 },
  { STATE_ID: '49', unemployment: 7.65 },
  { STATE_ID: '50', unemployment: 8.01 },
  { STATE_ID: '51', unemployment: 7.62 },
  { STATE_ID: '53', unemployment: 7.77 },
  { STATE_ID: '54', unemployment: 8.49 },
  { STATE_ID: '55', unemployment: 9.42 },
  { STATE_ID: '56', unemployment: 7.59 }
];
```

### Mapbox Boundaries lookup table

Each Boundaries tileset has its own feature lookup table in which each feature in that tileset is indexed. Lookup tables are designed to be used locally in your application. You can read more about feature lookup tables in the [Get started with Mapbox Boundaries](/help/tutorials/get-started-enterprise-boundaries/#about-feature-lookup-tables) guide.

The code snippet below illustrates how to import the feature lookup table from a file hosted in the application, then make the API request when the map loads, retrieve the contents of the lookup table, and print the response in the console. You will need to replace `./path/to/lookup/table` with the path to the appropriate lookup table, available in the reference documentation that is provided with Boundaries access.

```js
const lookupTable = require('./path/to/lookup/table')
map.on('load', function () {
  createViz(lookupTable);
});

function createViz(lookupData) {
  var dataValues = lookupData.data;
  console.log(dataValues);
}
```

Explore the response in the console to learn more about what is included in the lookup tables and better understand how you'll be using it in the next step.

### Feature state

**Feature state** is a set of attributes that can be dynamically assigned to a feature on the map. The [Mapbox GL JS feature state](https://www.mapbox.com/mapbox-gl-js/api/#map#setfeaturestate) API can be used to dynamically style the features of a vector or GeoJSON source, enabling new ways to handle map interactivity, data joins, and time series animations.

Building on the `createViz` function that was defined in the previous step, add the Mapbox Boundaries admin-1 tileset as a source named `statesData`.

{{
<Note
  imageComponent={<BookImage />}
>
  <p>Find the complete list of Mapbox Boundaries tilesets in the <a href="https://www.mapbox.com/vector-tiles/enterprise-boundaries-v2">reference documentation</a>.</p>
</Note>
}}

Then, create a new function called `setStates` within `createViz` to set the feature state. To join the local unemployment data to the vector tile boundary data, you'll need a property that can be used to match like features between the local and vector data. In the Boundaries feature lookup table, the information for each US state is in an object identified with a unique string using the following convention: `US` (for the United States) + `A1` (for Admin 1) + some number (unique for each state). In the _local data_, each state is represented with only a number. But this number corresponds with the numbers in the feature lookup table, so you can join the JSON unemployment data with the corresponding vector features where the object's identifier === `USA1` + `STATE_ID`.

Feature state requires knowing the `id` for each vector feature. This unique identifier must consist of only integers. In the Mapbox Boundaries lookup tables, `id_int` is this unique integer-only identifier. To get the vector tile feature `id` to set the feature state, you end up with `id: dataValues["USA1" + row["STATE_ID"]].id_int` to find the object in the `dataValues` from the lookup table with the identifier equal to `"USA1" + row["STATE_ID"]` and then getting the value of the `id_int` property.

Finally, you'll wait until the `statesData` source has been added to the map before calling your custom `setState` function to set the feature state.

```js
function createViz(lookupData) {
  var dataValues = lookupData.data;

  // Add Mapbox Boundaries source for state polygons.
  map.addSource('statesData', {
    type: 'vector',
    url: 'mapbox://mapbox.enterprise-boundaries-a1-v2'
  });

  // Join the JSON unemployment data with the corresponding vector features where
  // feautre.id === 'USA1' + `STATE_ID`.
  function setStates(e) {
    localData.forEach(function(row) {
      map.setFeatureState({ source: 'statesData', sourceLayer: 'boundaries_admin_1', id: dataValues['USA1' + row.STATE_ID].id_int }, { unemployment: row.unemployment });
    });
  }

  // Check if `statesData` source is loaded.
  function setAfterLoad(e) {
    if (e.sourceId === 'statesData' && e.isSourceLoaded) {
      setStates();
      map.off('sourcedata', setAfterLoad);
    }
  }

  // If `statesData` source is loaded, call `setStates()`.
  if (map.isSourceLoaded('statesData')) {
    setStates();
  } else {
    map.on('sourcedata', setAfterLoad);
  }
}
```

### Data-driven styling with expressions

Now that the local data and the vector data in the Mapbox Boundaries tileset have been joined, you can style the features in the Boundaries tileset according to the unemployment value from your local data. Inside the `createViz` function, add a new layer using `map.addLayer()`. The source will be `statesData` (added in the previous step), and the `source-layer` will be `boundaries_admin_1`.

You can use expressions to set the fill color of each feature according to the unemployment value found in the feature state. Mapbox GL JS expressions uses a Lisp-like syntax, represented using JSON arrays. Expressions follow this format:

```
[expression_name, argument_0, argument_1, ...]
```

The `expression_name` is the **expression operator**, for example, you would use [`'*'`](https://www.mapbox.com/mapbox-gl-js/style-spec/#expressions-*) to multiply two arguments or [`'case'`](https://www.mapbox.com/mapbox-gl-js/style-spec/#expressions-case) to create conditional logic. For a complete list of all available expressions see the [Mapbox Style Specification](https://www.mapbox.com/mapbox-gl-js/style-spec/#expressions).

The **arguments** are either _literal_ (numbers, strings, or boolean values) or else themselves expressions. The number of arguments varies based on the expression.

In this example, you'll use a combination of expressions to style the data as a choropleth map:

- [`case`](https://www.mapbox.com/mapbox-gl-js/style-spec#expressions-case): Use the `case` expression to (1) check if the unemployment feature state property is not null, (2) if unemployment is not null, you'll assign the fill color according to the value of unemployment, (3) if it is null, you'll assign a fill color of `rgba(255, 255, 255, 0)`.
- [`feature-state`](https://www.mapbox.com/mapbox-gl-js/style-spec#expressions-feature-state): Use the `feature-state` expression to retrieve the value of the unemployment property in the current feature's state.
- [`!=`](https://www.mapbox.com/mapbox-gl-js/style-spec#expressions-!=): Use the `!=` expression to check if the feature state unemployment property is not equal to null.
- [`interpolate`](https://www.mapbox.com/mapbox-gl-js/style-spec#expressions-interpolate): Use the `interpolate` expression to assign a fill color to two different values of unemployment and infer a continuous, smooth set of fill colors between the stops.

When you put all these expressions together, your code will look like this:

```js
map.addLayer({
  id: 'states-join',
  type: 'fill',
  source: 'statesData',
  'source-layer': 'boundaries_admin_1',
  paint: {
    'fill-color':
    ['case',
      ['!=', ['feature-state', 'unemployment'], null],
      ['interpolate', ['linear'], ['feature-state', 'unemployment'], 4, 'rgba(222,235,247,1)', 14, 'rgba(49,130,189,1)'],
      'rgba(255, 255, 255, 0)'
    ]
  }
}, 'waterway-label');
```

## Final product

You created a choropleth map using data-joins and Mapbox Boundaries.

![final choropleth map using Boundaries, local data, and expressions](/help/img/data/eb-data-join-final.png)

Here's the full code:

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset='utf-8' />
    <title>Join local JSON data with vector tile geometries</title>
    <meta name='viewport' content='initial-scale=1,maximum-scale=1,user-scalable=no' />
    <script src='https://api.tiles.mapbox.com/mapbox-gl-js/{{constants.VERSION_MAPBOXGLJS}}/mapbox-gl.js'></script>
    <link href='https://api.tiles.mapbox.com/mapbox-gl-js/{{constants.VERSION_MAPBOXGLJS}}/mapbox-gl.css' rel='stylesheet' />
    <style>
      body {
        margin: 0;
        padding: 0;
      }

      #map {
        position: absolute;
        top: 0;
        bottom: 0;
        width: 100%;
      }
    </style>
  </head>
  <body>
    <div id='map'></div>
    <script>
      mapboxgl.accessToken = '{{ <UserAccessToken /> }}';
      var map = new mapboxgl.Map({
        container: 'map',
        style: 'mapbox://styles/mapbox/light-v{{constants.VERSION_LIGHT_STYLE}}',
        center: [-99.9, 41.5],
        zoom: 1
      });

      // Join local JSON data with vector tile geometry
      // unemployment rate in 2009
      // Source https://data.bls.gov/timeseries/LNS14000000
      var maxValue = 14;
      var localData = [
        { STATE_ID: '01', unemployment: 13.17 },
        { STATE_ID: '02', unemployment: 9.5 },
        { STATE_ID: '04', unemployment: 12.15 },
        { STATE_ID: '05', unemployment: 8.99 },
        { STATE_ID: '06', unemployment: 11.83 },
        { STATE_ID: '08', unemployment: 7.52 },
        { STATE_ID: '09', unemployment: 6.44 },
        { STATE_ID: '10', unemployment: 5.17 },
        { STATE_ID: '12', unemployment: 9.67 },
        { STATE_ID: '13', unemployment: 10.64 },
        { STATE_ID: '15', unemployment: 12.38 },
        { STATE_ID: '16', unemployment: 10.13 },
        { STATE_ID: '17', unemployment: 9.58 },
        { STATE_ID: '18', unemployment: 10.63 },
        { STATE_ID: '19', unemployment: 8.09 },
        { STATE_ID: '20', unemployment: 5.93 },
        { STATE_ID: '21', unemployment: 9.86 },
        { STATE_ID: '22', unemployment: 9.81 },
        { STATE_ID: '23', unemployment: 7.82 },
        { STATE_ID: '24', unemployment: 8.35 },
        { STATE_ID: '25', unemployment: 9.1 },
        { STATE_ID: '26', unemployment: 10.69 },
        { STATE_ID: '27', unemployment: 11.53 },
        { STATE_ID: '28', unemployment: 9.29 },
        { STATE_ID: '29', unemployment: 9.94 },
        { STATE_ID: '30', unemployment: 9.29 },
        { STATE_ID: '31', unemployment: 5.45 },
        { STATE_ID: '32', unemployment: 4.21 },
        { STATE_ID: '33', unemployment: 4.27 },
        { STATE_ID: '34', unemployment: 4.09 },
        { STATE_ID: '35', unemployment: 7.83 },
        { STATE_ID: '36', unemployment: 8.01 },
        { STATE_ID: '37', unemployment: 9.34 },
        { STATE_ID: '38', unemployment: 11.23 },
        { STATE_ID: '39', unemployment: 7.08 },
        { STATE_ID: '40', unemployment: 11.22 },
        { STATE_ID: '41', unemployment: 6.2 },
        { STATE_ID: '42', unemployment: 9.11 },
        { STATE_ID: '44', unemployment: 10.42 },
        { STATE_ID: '45', unemployment: 8.89 },
        { STATE_ID: '46', unemployment: 11.03 },
        { STATE_ID: '47', unemployment: 7.35 },
        { STATE_ID: '48', unemployment: 8.92 },
        { STATE_ID: '49', unemployment: 7.65 },
        { STATE_ID: '50', unemployment: 8.01 },
        { STATE_ID: '51', unemployment: 7.62 },
        { STATE_ID: '53', unemployment: 7.77 },
        { STATE_ID: '54', unemployment: 8.49 },
        { STATE_ID: '55', unemployment: 9.42 },
        { STATE_ID: '56', unemployment: 7.59 }
      ];

      const lookupTable = require('./path/to/lookup/table')
      map.on('load', function () {
        createViz(lookupTable);
      });

      function createViz(lookupData) {
        var dataValues = lookupData.data;
        // Add Mapbox Boundaries source for state polygons.
        map.addSource('statesData', {
          type: 'vector',
          url: 'mapbox://mapbox.enterprise-boundaries-a1-v2'
        });

        // Add layer from the vector tile source with data-driven style
        // Use a feature-state dependent expression to compute the green color band based on
        //  the unemployment percentage
        map.addLayer({
          id: 'states-join',
          type: 'fill',
          source: 'statesData',
          'source-layer': 'boundaries_admin_1',
          paint: {
            'fill-color':
            ['case',
              ['!=', ['feature-state', 'unemployment'], null],
              ['interpolate', ['linear'], ['feature-state', 'unemployment'], 4, 'rgba(222,235,247,1)', 14, 'rgba(49,130,189,1)'],
              'rgba(255, 255, 255, 0)'
            ]
          }
        }, 'waterway-label');

        // Join the JSON unemployment data with the corresponding vector features where
        // feautre.id === 'USA1' + `STATE_ID`.
        function setStates(e) {
          localData.forEach(function(row) {
            map.setFeatureState({ source: 'statesData', sourceLayer: 'boundaries_admin_1', id: dataValues['USA1' + row.STATE_ID].id_int }, { unemployment: row.unemployment });
          });
        }

        // Check if `statesData` source is loaded.
        function setAfterLoad(e) {
          if (e.sourceId === 'statesData' && e.isSourceLoaded) {
            setStates();
            map.off('sourcedata', setAfterLoad);
          }
        }

        // If `statesData` source is loaded, call `setStates()`.
        if (map.isSourceLoaded('statesData')) {
          setStates();
        } else {
          map.on('sourcedata', setAfterLoad);
        }
      }
    </script>
  </body>
</html>
```

## Next steps

Learn more about how you can use Mapbox Boundaries.

### More Mapbox Boundaries tutorials

Explore our other Mapbox Boundaries tutorials:

- [Point-in-polygon query with Mapbox Boundaries](/help/tutorials/point-in-polygon-query-with-enterprise-boundaries/): Determine what polygons exist at a single point using the Mapbox Tilequery API.
- [Extend Mapbox Boundaries](/help/tutorials/extend-enterprise-boundaries/): You can extend Mapbox Boundaries with any custom data you need for your application. This could mean adding school district, city, market, or property boundaries to your application &mdash; all with the same performance and API features of the native product.

### Advanced use cases

You can also explore this [example](https://www.mapbox.com/labs-sandbox-demos/vt_polygons/), which uses the concepts outlined in both this data-join tutorial and the [Point-in-polygon query](/help/tutorials/point-in-polygon-query-with-enterprise-boundaries/) tutorial to create an application that features an interactive choropleth map.

![an end to end example using the data-join technique and Tilequery API](/help/img/data/enterprise-boundaries-choropleth-demo.gif)
