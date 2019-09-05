---
title: Find elevations with the Tilequery API
description: Use the Mapbox Tilequery API and the Mapbox Terrain tileset to create an app that returns the elevation at a specified coordinate.
thumbnail: tilequeryElevationMarker
topics:
- data
- web apps
level: 2
language:
- JavaScript
prereq: Familiarity with front-end development concepts.
prependJs:
  - "import Note from '@mapbox/dr-ui/note';"
  - "import BookImage from '@mapbox/dr-ui/book-image';"
  - "import Icon from '@mapbox/mr-ui/icon';"
  - "import DemoIframe from '@mapbox/dr-ui/demo-iframe';"
  - "import UserAccessToken from '../../components/user-access-token';"
  - "import * as constants from '../../constants';"
  - "import AppropriateImage from '../../components/appropriate-image';"
contentType: tutorial
---

In this tutorial, you will use the [Mapbox Tilequery API](https://docs.mapbox.com/api/maps/#tilequery) and the [Mapbox Terrain vector tileset](https://docs.mapbox.com/vector-tiles/reference/mapbox-terrain-v2/) to create an app that, when a user clicks a point on the map, returns the elevation at that point.

{{
  <DemoIframe src="/help/demos/find-elevations-with-tilequery-api/index.html" />
}}

## Getting started
To complete this tutorial, you will need:

- **A Mapbox access token.** Your Mapbox access tokens are on your [Account page](https://account.mapbox.com/).
- **Mapbox GL JS.** [Mapbox GL JS](https://docs.mapbox.com/mapbox-gl-js/overview/) is a JavaScript API for building web maps.
- **Mapbox Tilequery API.** The [Tilequery API](https://docs.mapbox.com/api/maps/#tilequery) allows you to retrieve data about specific features from a vector tileset, based on a given latitude and longitude.  
- **Mapbox Terrain vector tileset.** The [Mapbox Terrain](https://docs.mapbox.com/vector-tiles/reference/mapbox-terrain-v2/) vector tileset provides terrain data, including [elevation contours](https://docs.mapbox.com/vector-tiles/reference/mapbox-terrain-v2/#elevation).
- **jQuery.** [jQuery](https://jquery.com/) is a JavaScript library you will use to add your API request to the application.
- **A text editor.** Use the text editor of your choice for writing HTML, CSS, and JavaScript.

## Create a map
To get started, you will create a map using [Mapbox GL JS](https://docs.mapbox.com/mapbox-gl-js/api/).

Open your text editor and create a new file named `index.html`. Set up this new HTML file by pasting the following code into your text editor. This code creates the structure of the page. This code also imports Mapbox GL JS and jQuery in the `<head>` of the page. The Mapbox GL JS JavaScript and CSS files allow you to use Mapbox GL JS functionality and style, while jQuery will allow you to use [Ajax](https://api.jquery.com/jquery.ajax/) to parse your Tilequery API call.

There is also a `<div>` element with the ID `map` in the `<body>` of the page. This `<div>` is the container in which the map will be displayed on the page.

```html
<!DOCTYPE html>
<html>

<head>
  <meta charset='utf-8' />
  <title>Find elevations with the Tilequery API</title>
  <meta name='viewport' content='initial-scale=1,maximum-scale=1,user-scalable=no' />
  <script src='https://api.tiles.mapbox.com/mapbox-gl-js/{{constants.VERSION_MAPBOXGLJS}}/mapbox-gl.js'></script>
  <link href='https://api.tiles.mapbox.com/mapbox-gl-js/{{constants.VERSION_MAPBOXGLJS}}/mapbox-gl.css' rel='stylesheet' />
  <script
  src='https://code.jquery.com/jquery-3.4.1.min.js'></script>
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
      container: 'map', // Specify the container ID
      style: 'mapbox://styles/mapbox/outdoors-v{{constants.VERSION_OUTDOORS_STYLE}}', // Specify which map style to use
      center: [-122.43877, 37.75152], // Specify the starting position [lng, lat]
      zoom: 11.5 // Specify the starting zoom
    });
  </script>
  
</body>

</html>    
```

This Mapbox GL JS code sets the style for the map to [Mapbox Outdoors](https://docs.mapbox.com/api/maps/#mapbox-styles), gives it coordinates on which to center, and sets a zoom level.

Save your changes. Open the HTML file in your browser to see the rendered map, which is centered on San Francisco.

## Get coordinates when a user clicks
In this app, the coordinates used in the Tilequery API request will be generated when a user clicks on the map. To get these coordinates, you will create a `map.on('click')` function that gets the longitude and the latitude at the clicked location. Add the following JavaScript above the closing `</script>` tag in your HTML file:

```js
// Create variables for the latitude and longitude
var lng;
var lat;

map.on('click', function(e) {
  // When the map is clicked, set the lng and lat variables equal to the lng and lat properties in the returned lngLat object
  lng = e.lngLat.lng;
  lat = e.lngLat.lat;
  console.log(lng + ', ' + lat);
});
```

When the map is clicked, the returned event includes a Mapbox GL JS [`lngLat` object](https://docs.mapbox.com/mapbox-gl-js/api/#lnglat), which includes the longitude and latitude of the clicked point. The `map.on('click')` function sets the `lng` and `lat` variables equal to these properties.

Save your work, then refresh your browser page and open the browser's developer tools. When you click on the map, your app will print the clicked point's longitude and latitude to the JavaScript console.

{{
<AppropriateImage imageId="tilequeryElevationLngLatOnClick" alt="Screenshot showing two coordinate pairs printed to the developer console" />
}}

## Add the sidebar

In the `<body>` of your HTML, add a new `<div>`. This `<div>` will be used to show the clicked point's longitude, latitude, and elevation:

```html
<div class="eleInfo">
  <div>Longitude:&nbsp;<span id='lng'></span></div>
  <div>Latitude:&nbsp;<span id='lat'></span></div>
  <div>Elevation:&nbsp;<span id='ele'></span></div>
</div>
```

To style the new `<div>`, add the following CSS to the `<style>` section of your HTML:

```css
.eleInfo {
  position: absolute;
  font-family: sans-serif;
  margin-top: 5px;
  margin-left: 5px;
  padding: 5px;
  width: 200px;
  border: 2px solid black;
  font-size: 20px;
  color: #222;
  background-color: #fff;
}
```

Finally, create three new variables that you will use to target the new `<span>` IDs. Add the following code in your JavaScript, below the `lng` and `lat` variables:

```js
var lngDisplay = document.getElementById('lng');
var latDisplay = document.getElementById('lat');
var eleDisplay = document.getElementById('ele');
```

Save your work and refresh the page. The new sidebar will be on the left side of the page. In an upcoming step, you will use the `<span>` IDs that you created to display the longitude, latitude, and elevation in the sidebar.  

{{
<AppropriateImage imageId="tilequeryElevationSidebar" alt="Screenshot showing a sidebar on the map that contains the words Longitude, Latitude, and Elevation" />
}}

## Tilequery API request format
The [Mapbox Tilequery API](https://docs.mapbox.com/api/maps/#tilequery) allows you to retrieve data about specific features from a vector tileset, based on a given latitude and longitude.

A Tilequery request has two **required** two parameters:
- **`tileset_id`:** The identifier of the tileset being queried.
- **`{lon, lat}`:** The coordinates of the query point.

The Tilequery API also accepts several **optional** parameters. In this tutorial, you will use two optional parameters:
- **`limit`:** This parameter allows you to specify the maximum number of results that a query can return. The default number of results is five, and the maximum number is 50.
- **`layers`:** This parameter allows you to only return results from specific layers in the queried tileset.

An example call to the Tilequery API that has a `limit` of 50 results and only returns results from the `contour` layer looks like:

```
https://api.mapbox.com/v4/mapbox.mapbox-terrain-v2/tilequery/-105.01109,39.75953.json?layers=contour&limit=50&access_token={{ <UserAccessToken /> }}
```

A Tilequery API request returns a [GeoJSON `FeatureCollection`](https://tools.ietf.org/html/rfc7946#section-3.3) of features at or near the geographic point described by `{lon},{lat}`. To learn more about the Tilequery API, its other optional parameters, and its response object, explore the [Tilequery API documentation](https://docs.mapbox.com/api/maps/#tilequery).

## Mapbox Terrain tileset
In this tutorial, you will use the Tilequery API to query the [Mapbox Terrain](https://docs.mapbox.com/vector-tiles/reference/mapbox-terrain-v2/) vector tileset, which includes features like topography, hillshades, and landcover. Specifically, you will use the `layers` parameter to return features in the `contour` [source layer](https://docs.mapbox.com/help/glossary/source-layer/), which contain a property called [`ele`](https://docs.mapbox.com/vector-tiles/reference/mapbox-terrain-v2/#elevation). This property is the elevation value in meters, and is mapped to 10 meter height increments.

In the Mapbox Terrain tileset, `contour`s are comprised of stacked polygons. This means that most Tilequery API requests that query the Mapbox Terrain tileset will return multiple features from the `contour` layer. Because the elevation data you want is included in the `contour` layer, you will need to parse the returned GeoJSON to isolate the features from the `contour` layer and find the highest elevation value.

{{<Note title="Elevation data limitations in the Mapbox Terrain tileset" imageComponent={<BookImage />}>}}
The Tilequery API's `limit` parameter allows 50 or fewer features in a response. Since this tutorial uses the Mapbox Terrain vector tileset, which includes elevation data at 10 meter increments, 50 returned features may not be enough to return the largest value for some locations at high elevations.

Also, since the elevations are returned in 10 meter increments, the results may lose some nuance. For example, a hill that is 264 meters high would return a highest elevation of 260 meters. Mapbox does not have any other vector data sources with more precise elevation data than is available in the Terrain tileset.

If you are using the Tilequery API for areas with steep elevation changes, or if you require precise elevations, we recommend that you use the Tilequery API to query a custom tileset that contains this information.  
{{</Note>}}

## Add the Tilequery API call
You have already created variables that capture the longitude and latitude when a user clicks on the map. In this step, you will use these `lng` and `lat` variables in a call to the [Tilequery API](https://docs.mapbox.com/api/maps/#tilequery).

Write a function `getElevation()` that uses the `lng` and `lat` values to construct a Tilequery API request, then uses Ajax to send the request and retrieve the results. Add the following code to your JavaScript, before the closing `</script>` tag:

```js
function getElevation() {
  // Construct the API request
  var query = 'https://api.mapbox.com/v4/mapbox.mapbox-terrain-v2/tilequery/' + lng + ',' + lat + '.json?layers=contour&limit=50&access_token=' + mapboxgl.accessToken;
  $.ajax({
    method: 'GET',
    url: query,
  }).done(function(data) {
    // Get all the returned features
    var allFeatures = data.features;
    console.log(allFeatures);
    // Create an empty array to add elevation data to
    var elevations = [];
    // For each returned feature, add elevation data to the elevations array
    for (i = 0; i < allFeatures.length; i++) {
      elevations.push(allFeatures[i].properties.ele);
    }
    console.log(elevations);
    // In the elevations array, find the largest value
    var highestElevation = Math.max(...elevations);
    console.log(highestElevation);
  });
}
```

The Tilequery API returns feature objects. Since the feature objects in this query come from the `contour` layer, each of them contains a `properties.ele` value.

For each item in `allFeatures`, this code snippet takes the `properties.ele` value and pushes it to the `elevations` array. Then, using [`Math.max`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math/max) and [spread syntax](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax) `(...elevations)`, it sets the `highestElevation` variable to the largest value in the `elevations` array.

Now, you need to call `getElevation()` when a user clicks on the map. Update the `map.on('click')` function:

```js
map.on('click', function(e) {
  lng = e.lngLat.lng;
  lat = e.lngLat.lat;
  
  getElevation();
});
```

Save your changes and open your developer tools. Refresh the page in your browser and click on the map. On click, three items will be printed out to the console:
- `allFeatures`: Contains all the feature objects returned by the call to the Tilequery API. You can explore each feature object to see `properties.ele` for that feature.
- `elevations`: Contains every `properties.ele` value.
- `highestElevation`: The largest value in `elevations`, and therefore the highest point returned by the Tilequery API for the requested coordinates.

{{
<AppropriateImage imageId="tilequeryElevationElevationOnClick" alt="Screenshot showing the browser's develper tools, to which all the feature objects, their elevations, and the highest returned elevation have been printed" />
}}

## Display the returned values
Now that you have seen the results of the Tilequery API request printed to the console, your next step is to display them in the sidebar that you created earlier. Update the `getElevation()` function:

```js
function getElevation() {
  // make API request
  var query = 'https://api.mapbox.com/v4/mapbox.mapbox-terrain-v2/tilequery/' + lng + ',' + lat + '.json?layers=contour&limit=50&access_token=' + mapboxgl.accessToken;
  $.ajax({
    method: 'GET',
    url: query,
  }).done(function(data) {
    // Display the longitude and latitude values
    lngDisplay.textContent = lng.toFixed(2);
    latDisplay.textContent = lat.toFixed(2);
    // Get all the returned features
    var allFeatures = data.features;
    // Create an empty array to add elevation data to
    var elevations = [];
    // For each returned feature, add elevation data to the elevations array
    for (i = 0; i < allFeatures.length; i++) {
      elevations.push(allFeatures[i].properties.ele);
    }
    // In the elevations array, find the largest value
    var highestElevation = Math.max(...elevations);
    // Display the largest elevation value
    eleDisplay.textContent = highestElevation + ' meters';
  });
}
```

This updated function sets the value of `lngDisplay` and `latDisplay` to the clicked longitude and latitude respectively, and uses [`toFixed(2)`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/toFixed) to limit the displayed value to two decimal points. It also sets the value of `eleDisplay` to `highestElevation`.

Save your changes and refresh the page in your browser. Now, when you click a location on the map, its longitude, latitude, and elevation will display in the sidebar.

{{
<AppropriateImage imageId="tilequeryElevationSidebarDisplay" alt="Screenshot showing the sidebar, with a clicked point's longitude, latitude, and elevation displayed" />
}}

## Add a marker to the clicked location

The final step is to add a marker to the map at the coordinates where the user clicks. This will help the user better visualize the location that they are getting coordinates and elevation data for.

Add the following code to your JavaScript, before the `map.on('click')` function:

```js
var marker = new mapboxgl.Marker({
  'color': '#314ccd'
});
```

You can use the Mapbox GL JS [`lngLat` object](https://docs.mapbox.com/mapbox-gl-js/api/#lnglat) that is returned when the map is clicked to set the marker's location. To draw the marker on the map at the clicked coordinates, add the following code inside of your `map.on('click')` function:

```js
marker.setLngLat(e.lngLat).addTo(map);
```

Save your work and refresh the page. Now when you click on the map, you will see a blue marker at the clicked coordinates.

{{
<AppropriateImage imageId="tilequeryElevationMarker" alt="Screenshot showing the map with a marker at the clicked location" />
}}

## Final product
You have created an app that returns a clicked point's elevation and displays it on the map.

{{
  <DemoIframe src="/help/demos/find-elevations-with-tilequery-api/index.html" />
}}

The final HTML file will look like the following:

```html
<!DOCTYPE html>
<html>

<head>
  <meta charset='utf-8' />
  <title>Find elevations with the Tilequery API</title>
  <meta name='viewport' content='initial-scale=1,maximum-scale=1,user-scalable=no' />
  <script src='https://api.tiles.mapbox.com/mapbox-gl-js/{{constants.VERSION_MAPBOXGLJS}}/mapbox-gl.js'></script>
  <link href='https://api.tiles.mapbox.com/mapbox-gl-js/{{constants.VERSION_MAPBOXGLJS}}/mapbox-gl.css' rel='stylesheet' />
  <script
  src='https://code.jquery.com/jquery-3.4.1.min.js'></script>
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
    
    .eleInfo {
      position: absolute;
      font-family: sans-serif;
      margin-top: 5px;
      margin-left: 5px;
      padding: 5px;
      width: 200px;
      border: 2px solid black;
      font-size: 20px;
      color: #222;
      background-color: #fff;
    }
  </style>
</head>

<body>

  <div id='map'></div>
  <div class="eleInfo">
    <div>Longitude:&nbsp;<span id='lng'></span></div>
    <div>Latitude:&nbsp;<span id='lat'></span></div>
    <div>Elevation:&nbsp;<span id='ele'></span></div>
  </div>
  <script>
    mapboxgl.accessToken = '{{ <UserAccessToken /> }}';
    var map = new mapboxgl.Map({
      container: 'map', // Specify the container ID
      style: 'mapbox://styles/mapbox/outdoors-v{{constants.VERSION_OUTDOORS_STYLE}}', // Specify which map style to use
      center: [-122.43877, 37.75152], // Specify the starting position [lng, lat]
      zoom: 11.5 // Specify the starting zoom
    });
    
    var lng;
    var lat;
    var lngDisplay = document.getElementById('lng');
    var latDisplay = document.getElementById('lat');
    var eleDisplay = document.getElementById('ele');
    
    var marker = new mapboxgl.Marker({
      'color': '#314ccd'
    });

    map.on('click', function(e) {
      // Use the returned LngLat object to set the marker location
      // https://docs.mapbox.com/mapbox-gl-js/api/#lnglat
      marker.setLngLat(e.lngLat).addTo(map);
      
      // Create variables set to the LngLat object's lng and lat properties
      lng = e.lngLat.lng;
      lat = e.lngLat.lat;
      
      getElevation();
    });

    function getElevation() {
      // Make the API request
      var query = 'https://api.mapbox.com/v4/mapbox.mapbox-terrain-v2/tilequery/' + lng + ',' + lat + '.json?layers=contour&limit=50&access_token=' + mapboxgl.accessToken;
      $.ajax({
        method: 'GET',
        url: query,
      }).done(function(data) {
        // Display the longitude and latitude values
        lngDisplay.textContent = lng.toFixed(2);
        latDisplay.textContent = lat.toFixed(2);
        // Get all the returned features
        var allFeatures = data.features;
        // Create an empty array to add elevation data to
        var elevations = [];
        // For each returned feature, add elevation data to the elevations array
        for (i = 0; i < allFeatures.length; i++) {
          elevations.push(allFeatures[i].properties.ele);
        }
        // In the elevations array, find the largest value
        var highestElevation = Math.max(...elevations);
        // Display the largest elevation value
        eleDisplay.textContent = highestElevation + ' meters';
      });
    }
  </script>

</body>

</html>
```

## Next steps
To build on top of the tools and techniques you used in this tutorial, explore the following resources:
- Explore the [Tilequery API documentation](https://docs.mapbox.com/api/maps/#tilequery) for more information on how to use the optional parameters.
- Learn how to use the Tilequery API outside of a map with the [Create a timezone finder with the Tilequery API](https://docs.mapbox.com/help/tutorials/create-a-timezone-finder-with-mapbox-tilequery-api/) tutorial.
- Learn how to use the Tilequery API in conjunction with the Mapbox Geocoding API to query results from a custom tileset with the [Make a healthy food finder with the Tilequery API](https://docs.mapbox.com/help/tutorials/tilequery-healthy-food-finder/) tutorial.
- If using the Tilequery API to query the Mapbox Terrain vector tileset does not provide the level of elevation detail that you need, you can explore an [alternative method of retrieving elevation data](https://docs.mapbox.com/help/troubleshooting/access-elevation-data/#mapbox-terrain-rgb) using Mapbox Terrain-RGB, a raster tileset, instead.
