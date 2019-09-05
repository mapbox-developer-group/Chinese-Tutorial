---
title: Make a healthy food finder with the Tilequery API
description: Create a web app that uses the Mapbox Tilequery API in concert with the Mapbox Geocoding API to show all stores that sell food that are located within one mile of a query point.
thumbnail: tilequeryFoodDesertPopup
topics:
- data
- geocoding
- web apps
level: 2
language:
- JavaScript
prereq: Familiarity with front-end development concepts.
prependJs:
  - "import Note from '@mapbox/dr-ui/note';"
  - "import BookImage from '@mapbox/dr-ui/book-image';"
  - "import Icon from '@mapbox/mr-ui/icon';"
  - "import Button from '@mapbox/mr-ui/button';"
  - "import DemoIframe from '@mapbox/dr-ui/demo-iframe';"
  - "import UserAccessToken from '../../components/user-access-token';"
  - "import * as constants from '../../constants';"
  - "import AppropriateImage from '../../components/appropriate-image';"
  - "import { ColorSwatch } from '../../components/color-swatch';"
contentType: tutorial
---

This tutorial demonstrates how you can combine your own custom geospatial data, the Tilequery API, and Mapbox's global address and place data using the Geocoding API to create a cohesive, custom reverse search experience for your users.

In this tutorial, you will create a web app that shows all stores that sell food that are located within one mile of a query point. You will use **Mapbox GL JS** to create the interface, the **Mapbox Geocoding API** (in the form of the **Mapbox GL JS Geocoder plugin**) to set a query point, and the **Tilequery API** to find stores that are within one mile of that query point.

A person using this app could search for a location, then use the results to determine whether the area is a _food desert_. A [food desert](https://en.wikipedia.org/wiki/Food_desert) is an urban area in which at least 33% of the population live more than one mile from a supermarket or large grocery store. (For rural areas, the distance is more than 10 miles.) People who live in these food desert areas may have difficulty finding healthy foods. Identifying a food desert can be the first step toward solving the issue.

{{
  <DemoIframe src="/help/demos/tilequery-healthy-food-finder/index.html" />
}}

## Getting started
To complete this tutorial, you will need:

- **A Mapbox access token.** Your Mapbox access tokens are on your [Account page](https://account.mapbox.com/).
- **Mapbox GL JS.** [Mapbox GL JS](https://docs.mapbox.com/mapbox-gl-js/overview/) is a JavaScript API for building web maps.
- **A text editor.** Use the text editor of your choice for writing HTML, CSS, and JavaScript.
- **Data.** In this tutorial, you will use food store data from the [City of Denver Open Data Catalog](https://www.denvergov.org/opendata/dataset/city-and-county-of-denver-food-stores). The original file has been simplified by removing columns that are not relevant to this tutorial.

{{
<Button href="/help/demos/tilequery-healthy-food-finder/food_stores.csv" passthroughProps={{ download: "food_stores.csv" }} >
    <Icon name='arrow-down' inline={true} /> Download CSV
</Button>
}}

## Upload the data as a tileset
A [tileset](https://docs.mapbox.com/help/glossary/tileset/) is a collection of raster or vector data broken up into a uniform grid of square tiles. Tilesets are highly cacheable and load quickly, and help Mapbox maps load quickly. In this step, you will upload the food store location to Mapbox as a new tileset so that you can access it in later steps.

1. Log into [Mapbox Studio](https://studio.mapbox.com/) and navigate to the [Tilesets page](https://studio.mapbox.com/tilesets/).
1. Click the **New tileset** button.
1. Click the **Select a file** button and navigate to the location in which you saved the `food_stores.csv` file.
1. Select `food_stores.csv`, then click **Confirm**.  
1. When the upload successfully finishes, it will appear at the top of the custom tilesets list on your Tilesets page.
1. Click on the **Menu** button next to the new tileset's name. Find the _tileset ID_, which is the tileset's unique identifier. You will need to use this in a later step, so remember where you found it!

## Create a map
Next, you will create a map using [Mapbox GL JS](https://docs.mapbox.com/mapbox-gl-js/api/).

Open your text editor and create a new file named `index.html`. Set up this new HTML file by pasting the following code into your text editor. This code creates the structure of the page. This code also imports Mapbox GL JS and jQuery in the `<head>` of the page. The Mapbox GL JS JavaScript and CSS files allow you to use Mapbox GL JS functionality and style, while jQuery will allow you to use [Ajax](https://api.jquery.com/jquery.ajax/) to parse your Tilequery API call.

There is a `<div>` element with the ID `map` in the `<body>` of the page. This `<div>` is the container in which the map will be displayed on the page.

```html
<!DOCTYPE html>
<html>

<head>
  <meta charset='utf-8' />
  <title>Healthy food finder</title>
  <meta name='viewport' content='initial-scale=1,maximum-scale=1,user-scalable=no' />
  <!-- Import Mapbox GL JS -->
  <script src='https://api.tiles.mapbox.com/mapbox-gl-js/{{constants.VERSION_MAPBOXGLJS}}/mapbox-gl.js'></script>
  <link href='https://api.tiles.mapbox.com/mapbox-gl-js/{{constants.VERSION_MAPBOXGLJS}}/mapbox-gl.css' rel='stylesheet' />
  <!-- Import jQuery -->
  <script src='https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js'></script>
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
    mapboxgl.accessToken = '{{ <UserAccessToken /> }}'; // set the access token

    var map = new mapboxgl.Map({
      container: 'map', // The container ID
      style: 'mapbox://styles/mapbox/light-v10', // The map style to use
      center: [-105.0178157, 39.737925], // Starting position [lng, lat]
      zoom: 12 // Starting zoom level
    });
  </script>

</body>

</html>
```

This Mapbox GL JS code sets a style for the map, gives it coordinates on which to center, and sets a zoom level.

Save your changes. Open the HTML file in your browser to see the rendered map, which is centered on the city of Denver.

{{
<AppropriateImage imageId="tilequeryFoodDesertBaseMap" alt="Screenshot of the map that is generated by following the instructions in this step." />
}}

## Add the geocoder
The next step is to add a geocoder to the map using the [Mapbox GL JS Geocoder plugin](https://github.com/mapbox/mapbox-gl-geocoder). This plugin allows you to take advantage of the [Mapbox Geocoding API](https://docs.mapbox.com/api/search/#geocoding) within the context of Mapbox GL JS.

To add the geocoder to your map, first add the links to the geocoder plugin's JavaScript and CSS to the head of the HTML file:

```html
<script src='https://api.mapbox.com/mapbox-gl-js/plugins/mapbox-gl-geocoder/{{constants.VERSION_GLJS_GEOCODER_PLUGIN}}/mapbox-gl-geocoder.min.js'></script>
<link rel='stylesheet' href='https://api.mapbox.com/mapbox-gl-js/plugins/mapbox-gl-geocoder/{{constants.VERSION_GLJS_GEOCODER_PLUGIN}}/mapbox-gl-geocoder.css' type='text/css' />
```

Once these links have been added, you will be able to use the geocoder plugin in your app. Next, add the following code above the closing `</script>` tag in your HTML file.

```js
map.on('load', function() {
  var geocoder = new MapboxGeocoder({ // Initialize the geocoder
    accessToken: mapboxgl.accessToken, // Set the access token
    mapboxgl: mapboxgl, // Set the mapbox-gl instance
    zoom: 13, // Set the zoom level for geocoding results
    placeholder: "Enter an address or place name", // This placeholder text will display in the search bar
    bbox: [-105.116, 39.679, -104.898, 39.837] // Set a bounding box
  });
  // Add the geocoder to the map
  map.addControl(geocoder, 'top-left'); // Add the search box to the top left
});  
```

The `bbox` parameter in this code sets a _bounding box_, which means that the geocoder will not return any results that are outside of the specified area. The coordinates of this bounding box roughly describe the city of Denver. Learn more about the `bbox` parameter in the [Geocoding API documentation](https://docs.mapbox.com/api/search/#forward-geocoding).

Save your changes. Refresh the page in your browser, and you will see that a geocoder search box with custom text has been added to the map. When you type a search term into the box and select a result, the map flies to that location.

{{
<AppropriateImage imageId="tilequeryFoodDesertAddGeocoder" alt="Screenshot showing a map with a functional geocoder in the upper left corner." />
}}

## Place a marker on the map
Now you have a web app that flies to a result location when a user enters a location in the geocoder. Next, you will add a marker to the result location to show where this center point is.

Paste the following code into your file, right below `map.addControl(geocoder, 'top-left');`:

```js
var marker = new mapboxgl.Marker({'color': '#008000'}) // Create a new green marker

geocoder.on('result', function(data) { // When the geocoder returns a result
  var point = data.result.center; // Capture the result coordinates

    marker.setLngLat(point).addTo(map); // Add the marker to the map at the result coordinates

});
```

This code snippet initializes a new marker after a result is returned, then adds it to the map at search result's coordinates. Learn more about markers in the [Mapbox GL JS documentation](https://docs.mapbox.com/mapbox-gl-js/api/#marker).

Save your changes. Refresh the page in your browser and enter a location in the search box. When you choose a result, the map will fly to that location and add a green marker.

{{
<AppropriateImage imageId="tilequeryFoodDesertAddMarker" alt="Screenshot that shows a map with a green marker that shows the coordinates returned by the geocoder." />
}}

## Add the Tilequery API
In the last step, you created a variable named `point` that is the coordinates returned by a user's request to the Geocoding API. In this step, you will use this variable in a call to the [Tilequery API](https://docs.mapbox.com/api/maps/#tilequery).

### Tilequery API request format
The [Mapbox Tilequery API](https://docs.mapbox.com/api/maps/#tilequery) allows you to retrieve data about specific features from a vector tileset, based on a given latitude and longitude.

A Tilequery request requires two parameters: the `tileset_id` of the tileset being queried, and the `{lon, lat}` coordinates of the query point. The Tilequery API accepts an optional `radius` parameter, which is a distance in meters from the query point in which to search for features. It also accepts a `limit` parameter so that you can specify the maximum number of results that a query can return.

An example call to the Tilequery API that had a radius of 1,000 meters and a limit of 10 would look like:

```
https://api.mapbox.com/v4/mapbox.mapbox-streets-v8/tilequery/-105.01109,39.75953.json?radius=1000&limit=10&access_token={{ <UserAccessToken /> }}
```

A Tilequery API request returns a [GeoJSON `FeatureCollection`](https://tools.ietf.org/html/rfc7946#section-3.3) of features at or near the geographic point described by `{lon},{lat}` and within the distance described by the `radius` parameter.

### Set up the Tilequery API call
In the `geocoder.on('result')` method you wrote earlier, you will create three more variables, use them to create the Tilequery API request, and then use Ajax to make the Tilequery API call.

Now you will create variables for the tileset that the Tilequery API will query, the radius in which it should search, and the maximum number of results to return. Go back to your [Tilesets page](https://studio.mapbox.com/tilesets/) and find the _tileset ID_ of the tileset you created. After the `point` variable that you declared earlier, add these additional variables:
```js
var tileset = 'examples.dl46ljcs'; // replace this with the ID of the tileset you created
var radius = 1609; // 1609 meters is roughly equal to one mile
var limit = 50; // The maximum amount of results to return
```

Next, use these new variables to create a new variable for the Tilequery API request.

```js
var query = 'https://api.mapbox.com/v4/' + tileset + '/tilequery/' + point[0] + ',' + point[1] + '.json?radius=' + radius + '&limit= ' + limit + ' &access_token=' + mapboxgl.accessToken;
```

Next, you will use Ajax to make the Tilequery API call. Add the following code inside of the `geocoder.on('result')` call, before the closing curly brace. In the next step you will add a circle to the map for each store in the radius area, but for now you can view the results using `console.log()`.

```js
$.ajax({
  method: 'GET',
  url: query,
}).done(function(data) {
  console.log(data);
  // Code from the next step will go here
})
```

Save your changes and open your developer tools. Refresh the page in your browser and enter a location in the search box. When you select a result, the results of the call to the Tilequery API will print out to the console.

{{
<AppropriateImage imageId="tilequeryFoodDesertLogResults" alt="Screenshot showing a map. The browser's developer tools are open with the GeoJSON FeatureCollection results displayed." />
}}

## Display store locations
In the last step, you set up a Tilequery API call that sets the result coordinates of a request to the Geocoding API as the query point. Now that your query returns store locations as a result, you will use Mapbox GL JS to add a visual representation of each store's location to the map.

Add the following code to the end of your JavaScript, before the closing curly brace of the `map.on('load')` function.

```js
map.addSource('tilequery', { // Add a new source to the map style: https://docs.mapbox.com/mapbox-gl-js/api/#map#addsource
  type: "geojson",
  data: {
    "type": "FeatureCollection",
    "features": []
  }
});

map.addLayer({ // Add a new layer to the map style: https://docs.mapbox.com/mapbox-gl-js/api/#map#addlayer
  id: "tilequery-points",
  type: "circle",
  source: "tilequery", // Set the layer source
  paint: {
    "circle-stroke-color": "white",
    "circle-stroke-width": { // Set the stroke width of each circle: https://docs.mapbox.com/mapbox-gl-js/style-spec/#paint-circle-circle-stroke-width
      stops: [
        [0, 0.1],
        [18, 3]
      ],
      base: 5
    },
    "circle-radius": { // Set the radius of each circle, as well as its size at each zoom level: https://docs.mapbox.com/mapbox-gl-js/style-spec/#paint-circle-circle-radius
      stops: [
        [12, 5],
        [22, 180]
      ],
      base: 5
    },
    "circle-color": [ // Specify the color each circle should be
      'match', // Use the 'match' expression: https://docs.mapbox.com/mapbox-gl-js/style-spec/#expressions-match
      ['get', 'STORE_TYPE'], // Use the result 'STORE_TYPE' property
      'Convenience Store', '#FF8C00',
      'Convenience Store With Gas', '#FF8C00',
      'Pharmacy', '#FF8C00',
      'Specialty Food Store', '#9ACD32',
      'Small Grocery Store', '#008000',
      'Supercenter', '#008000',
      'Superette', '#008000',
      'Supermarket', '#008000',
      'Warehouse Club Store', '#008000',
      '#FF0000' // any other store type
    ]
  }
});
```

This code uses a Mapbox GL JS `match` expression to set the color of each circle based on the `STORE_TYPE` property:
- Grocery stores of any size, where shoppers are likely to find fresh produce and other healthy food, are set to {{<ColorSwatch color="#008000" />}}.
- Specialty food stores, which may or may not have fresh produce, are set to {{<ColorSwatch color="#9ACD32" />}}.
- Convenience stores, which often have food but rarely have fresh food, are set to {{<ColorSwatch color="#FF8C00" />}}.
- A store with any other `STORE_TYPE` is set to {{<ColorSwatch color="#FF0000" />}}.

Learn more about expressions and how to use them in the [Mapbox style specification](https://docs.mapbox.com/mapbox-gl-js/style-spec/#expressions).

Now that you have set the `tilequery` source up and added rules for the presentation of the points, you will reference this in the Ajax call you created in the last step. You will replace `console.log(resp);` so that the entire function is:

```js
$.ajax({ // Make the API call
  method: 'GET',
  url: query,
}).done(function(data) { // Use the response to populate the 'tilequery' source
  map.getSource('tilequery').setData(data);
})
```

Save your changes and refresh the page in your browser. When you search for a location, you will see the store locations populate on the map, colored according to the `match` expression.

{{
<AppropriateImage imageId="tilequeryFoodDesertStoreLocations" alt="Screenshot showing the colored circles that populated on the map after a successful Tilequery API call." />
}}

## Add popups for each store
The last step is to add popups to each store that list the store's name, type, address, and distance from the query point. Mapbox GL JS provides a [popup component](https://docs.mapbox.com/mapbox-gl-js/api/#popup) that allows you to customize popups according to your needs.

Add the following code to the end of your JavaScript, before the closing curly brace of the `map.on('load')` function:

```js
var popup = new mapboxgl.Popup; // Initialize a new popup

map.on('mouseenter', 'tilequery-points', function(e) {
  map.getCanvas().style.cursor = 'pointer'; // When the cursor enters a feature, set it to a pointer

  var title = '<h3>' + e.features[0].properties.STORE_NAME + '</h3>'; // Set the store name
  var storeType = '<h4>' + e.features[0].properties.STORE_TYPE + '</h4>'; // Set the store type
  var storeAddress = '<p>' + e.features[0].properties.ADDRESS_LINE1 + '</p>'; // Set the store address
  var obj = JSON.parse(e.features[0].properties.tilequery); // Get the feature's tilequery object (https://docs.mapbox.com/api/maps/#response-retrieve-features-from-vector-tiles)
  var distance = '<p>' + (obj.distance / 1609.344).toFixed(2) + ' mi. from location' + '</p>'; // Take the distance property, convert it to miles, and truncate it at 2 decimal places

  var lon = e.features[0].properties.longitude;
  var lat = e.features[0].properties.latitude;
  var coordinates = new mapboxgl.LngLat(lon, lat); // Create a new LngLat object (https://docs.mapbox.com/mapbox-gl-js/api/#lnglatlike)
  var content = title + storeType + storeAddress + distance; // All the HTML elements

  popup.setLngLat(coordinates) // Set the popup at the given coordinates
    .setHTML(content) // Set the popup contents equal to the HTML elements you created
    .addTo(map); // Add the popup to the map
})

map.on('mouseleave', 'tilequery-points', function() {
  map.getCanvas().style.cursor = ''; // Reset the cursor when it leaves the point
  popup.remove(); // Remove the popup when the cursor leaves the point
});
```

Save your changes and refresh the page in your browser. When the store locations populate on the map, a popup will display for each location when you mouse over it.

{{
<AppropriateImage imageId="tilequeryFoodDesertPopup" alt="Screenshot showing the map with a popup displayed over one store location." />
}}

## Final product

You created an app that uses the Tilequery API to augment the Mapbox geocoder to identify potential food deserts in the city of Denver.

{{
  <DemoIframe src="/help/demos/tilequery-healthy-food-finder/index.html" />
}}

The final HTML file will look like the following:

```html
<!DOCTYPE html>
<html>

<head>
  <meta charset='utf-8' />
  <title>Healthy food finder</title>
  <meta name='viewport' content='initial-scale=1,maximum-scale=1,user-scalable=no' />
  <script src='https://api.tiles.mapbox.com/mapbox-gl-js/{{constants.VERSION_MAPBOXGLJS}}/mapbox-gl.js'></script>
  <link href='https://api.tiles.mapbox.com/mapbox-gl-js/{{constants.VERSION_MAPBOXGLJS}}/mapbox-gl.css' rel='stylesheet' />
  <script src='https://api.mapbox.com/mapbox-gl-js/plugins/mapbox-gl-geocoder/{{constants.VERSION_GLJS_GEOCODER_PLUGIN}}/mapbox-gl-geocoder.min.js'></script>
  <link rel='stylesheet' href='https://api.mapbox.com/mapbox-gl-js/plugins/mapbox-gl-geocoder/{{constants.VERSION_GLJS_GEOCODER_PLUGIN}}/mapbox-gl-geocoder.css' type='text/css' />
  <script src='https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js'></script>
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
      style: 'mapbox://styles/mapbox/light-v10',
      center: [-105.0178157, 39.737925],
      zoom: 12
    });

    map.on('load', function() {
      var geocoder = new MapboxGeocoder({
        accessToken: mapboxgl.accessToken,
        mapboxgl: mapboxgl,
        zoom: 13,
        placeholder: "Enter an address or place name",
        bbox: [-105.116, 39.679, -104.898, 39.837]
      });

      map.addControl(geocoder, 'top-left');

      var marker = new mapboxgl.Marker({'color': '#008000'})

      geocoder.on('result', function(data) {

        var point = data.result.center;
        var tileset = 'examples.dl46ljcs';
        var radius = 1609;
        var limit = 50;
        var query = 'https://api.mapbox.com/v4/' + tileset + '/tilequery/' + point[0] + ',' + point[1] + '.json?radius=' + radius + '&limit= ' + limit + ' &access_token=' + mapboxgl.accessToken;

        marker.setLngLat(point).addTo(map);

        $.ajax({
          method: 'GET',
          url: query,
        }).done(function(data) {
          map.getSource('tilequery').setData(data);
        })
      });

      map.addSource('tilequery', {
        type: "geojson",
        data: {
          "type": "FeatureCollection",
          "features": []
        }
      });

      map.addLayer({
        id: "tilequery-points",
        type: "circle",
        source: "tilequery",
        paint: {
          "circle-stroke-color": "white",
          "circle-stroke-width": {
            stops: [
              [0, 0.1],
              [18, 3]
            ],
            base: 5
          },
          "circle-radius": {
            stops: [
              [12, 5],
              [22, 180]
            ],
            base: 5
          },
          "circle-color": [
            'match',
            ['get', 'STORE_TYPE'],
            'Convenience Store', '#FF8C00',
            'Convenience Store With Gas', '#FF8C00',
            'Pharmacy', '#FF8C00',
            'Specialty Food Store', '#9ACD32',
            'Small Grocery Store', '#008000',
            'Supercenter', '#008000',
            'Superette', '#008000',
            'Supermarket', '#008000',
            'Warehouse Club Store', '#008000',
            '#FF0000' // any other store type
          ]
        }
      });

      var popup = new mapboxgl.Popup;

      map.on('mouseenter', 'tilequery-points', function(e) {
        map.getCanvas().style.cursor = 'pointer';

        var title = '<h3>' + e.features[0].properties.STORE_NAME + '</h3>';
        var storeType = '<h4>' + e.features[0].properties.STORE_TYPE + '</h4>';
        var storeAddress = '<p>' + e.features[0].properties.ADDRESS_LINE1 + '</p>';
        var obj = JSON.parse(e.features[0].properties.tilequery);
        var distance = '<p>' + (obj.distance / 1609.344).toFixed(2) + ' mi. from location' + '</p>';

        var lon = e.features[0].properties.longitude;
        var lat = e.features[0].properties.latitude;
        var coordinates = new mapboxgl.LngLat(lon, lat);
        var content = title + storeType + storeAddress + distance;

        popup.setLngLat(coordinates)
          .setHTML(content)
          .addTo(map);
      })

      map.on('mouseleave', 'tilequery-points', function() {
        map.getCanvas().style.cursor = '';
        popup.remove();
      });

    })
  </script>

</body>

</html>

```

## Next steps
There are a lot of things you could do to build this app out more. You could:
- Add another custom tileset that has population-level data, which would allow you to investigate whether an area without many stores is truly underserved or if it doesn't have a large population. (See the [Visualize population density](https://docs.mapbox.com/mapbox-gl-js/example/visualize-population-density/) example.)
- Experiment with [expressions](https://docs.mapbox.com/mapbox-gl-js/style-spec/#expressions) in Mapbox GL JS to customize the store location results based on store type even further. (See the [Style circles with a data-driven property](https://docs.mapbox.com/mapbox-gl-js/example/data-driven-circle-colors/) example.)
- Create a toggle function that would allow you to only display results that are a certain store type, like "Supermarket" or "Convenience Store with Gas". (See the [Filter symbols by toggling a list](https://docs.mapbox.com/mapbox-gl-js/example/filter-markers/) example.)
