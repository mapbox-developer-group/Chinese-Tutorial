---
title: Get started with the Isochrone API
description: Create a web app using the Mapbox Isochrone API that allows users to visualize how far they could walk, bike, or drive within a given amount of time.
thumbnail: isochroneFinalProduct
topics:
- web apps
- navigation
level: 2
language:
- JavaScript
prereq: Familiarity with front-end development concepts.
prependJs:
  - "import DemoIframe from '@mapbox/dr-ui/demo-iframe';"
  - "import UserAccessToken from '../../components/user-access-token';"
  - "import * as constants from '../../constants';"
  - "import AppropriateImage from '../../components/appropriate-image';"
  - "import Note from '@mapbox/dr-ui/note';"
  - "import BookImage from '@mapbox/dr-ui/book-image';"
contentType: tutorial
---

This tutorial demonstrates how you can use the Mapbox Isochrone API, which uses Mapbox routing profiles and travel times, to create a web app that allows users to estimate how far they could travel by foot, bicycle, or car within a set amount of time.

{{
  <DemoIframe src="/help/demos/get-started-isochrone-api/index.html" />
}}

## Getting started
To complete this tutorial, you will need:

- **A Mapbox access token.** Your Mapbox access tokens are on your [Account page](https://account.mapbox.com/).
- **Mapbox GL JS.** [Mapbox GL JS](https://docs.mapbox.com/mapbox-gl-js/overview/) is a JavaScript API for building web maps.
- **Mapbox Isochrone API.** The [Isochrone API](https://docs.mapbox.com/api/navigation/#isochrone) computes areas that are reachable within a specified amount of time from a location, and returns the reachable regions as contours of polygons or lines that you can display on a map.   
- **Mapbox Assembly.** [Assembly](https://labs.mapbox.com/assembly/) is an open source CSS framework you will use to style the user interface for your app.
- **jQuery.** [jQuery](https://jquery.com/) is a JavaScript library you will use to add your API request to your application.
- **A text editor.** Use the text editor of your choice for writing HTML, CSS, and JavaScript.

## Using the Isochrone API
An Isochrone API request requires three parameters:

- **`profile`:** The Mapbox routing `profile` that the query should use. This can be `walking` for pedestrian and hiking travel times, `cycling` for travel times by bicycle, or `driving` for travel times by car.
- **`coordinates`:** A `{longitude,latitude}` coordinate pair around which to center the isochrone lines.
- **`contours_minutes`:** Times that describe the duration in minutes of the trip. This can be a comma-separated list of up to four times. The maximum duration is 60 minutes.

```
https://api.mapbox.com/isochrone/v1/mapbox/{profile}/{coordinates}.json?{contours_minutes}&access_token=YOUR_MAPBOX_ACCESS_TOKEN
```

The Isochrone API also accepts several optional parameters that can be used to customize the query. For this app, you will be using one optional parameter:

- `polygons`: This parameter specifies whether to return the contours as GeoJSON polygons or linestrings. When `polygons=true`, any contour that forms a ring is returned as a polygon.

To learn more about the Isochrone API and its other optional parameters, explore the [Isochrone API documentation](https://docs.mapbox.com/api/navigation/#isochrone).

This example query uses the `driving` routing profile, has a `contours_minutes` of 15, and has the `polygons` parameter set to `true`:

```
https://api.mapbox.com/isochrone/v1/mapbox/driving/-117.17282,32.71204?contours_minutes=15&polygons=true&access_token={{ <UserAccessToken /> }}
```

To see the JSON response to this query, you can paste it into your browser. The response's `geometry` object contains an array of `coordinates` that describe the outlines of the isochrone contour. The response also contains a `features` object that describes how the isochrone should be drawn, including its fill color and fill opacity. You will use the information returned by the Isochrone API to draw and style the contours of the returned isochrone to the app's map.

## Create a map
To start the app, you will create a map using [Mapbox GL JS](https://docs.mapbox.com/mapbox-gl-js/api/).

1. Open your text editor.
1. Create a new file named `index.html`.
1. Set up this new HTML file by pasting the following code into your text editor.

```html
<!DOCTYPE html>
<html>

<head>
  <meta charset='utf-8' />
  <title>Get started with the Isochrone API</title>
  <meta name='viewport' content='initial-scale=1,maximum-scale=1,user-scalable=no' />
  <!-- Import Mapbox GL JS  -->
  <script src='https://api.tiles.mapbox.com/mapbox-gl-js/{{constants.VERSION_MAPBOXGLJS}}/mapbox-gl.js'></script>
  <link href='https://api.tiles.mapbox.com/mapbox-gl-js/{{constants.VERSION_MAPBOXGLJS}}/mapbox-gl.css' rel='stylesheet' />
  <!-- Import Assembly -->
  <link href='https://api.mapbox.com/mapbox-assembly/{{constants.ASSEMBLY}}/assembly.min.css' rel='stylesheet'>
  <script src='https://api.mapbox.com/mapbox-assembly/{{constants.ASSEMBLY}}/assembly.js'></script>
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
  <!-- Create a container for the map -->
  <div id='map'></div>

  <script>
    // Add your Mapbox access token
    mapboxgl.accessToken = '{{ <UserAccessToken /> }}';
    var map = new mapboxgl.Map({
      container: 'map', // Specify the container ID
      style: 'mapbox://styles/mapbox/streets-v{{constants.VERSION_STREETS_STYLE}}', // Specify which map style to use
      center: [-77.0369,38.895], // Specify the starting position
      zoom: 11.5, // Specify the starting zoom
    });
  </script>
</body>

</html>
```

This code creates the structure of the page. It also imports Mapbox GL JS, Assembly, and jQuery in the `<head>` of the page. The Mapbox GL JS JavaScript and CSS files allow you to use Mapbox GL JS functionality and map style, and the Assembly CSS framework allows you to further refine the style of the non-map elements on the page. jQuery allows you to use [Ajax](https://api.jquery.com/jquery.ajax/) to parse your Isochrone API call.

There is a `<div>` element with the ID `map` in the `<body>` of the page. This `<div>` is the container in which the map will be displayed on the page.

Save your changes. Open the HTML file in your browser to see the rendered map, which is centered on the Mapbox headquarters in Washington D.C.

{{
<AppropriateImage imageId="isochroneRenderedMap" alt="Screenshot showing a Mapbox GL JS map rendered in the browser" />
}}

## Add the sidebar

Next, add a sidebar to the web app that will allow users to select a transportation profile and time duration.

In the `<body>` of your HTML, add a new `<div>`. This `<div>` holds the app's options and uses Assembly classes for styling.

{{<Note title="Using Assembly to style your app" imageComponent={<BookImage />}>}}
The code for the form uses [Assembly classes](https://labs.mapbox.com/assembly/) that provide CSS styling for the specified elements. For example, applying the classes `absolute fl my24 mx24 py24 px24 bg-gray-faint round` to the parent `div` sets its position to `absolute` and floats it to the left, gives it margin and padding of 24 pixels, sets the background to a light gray, and adds a border radius to round the corners. In your own app, you could also use plain CSS or the CSS framework of your choice to style the sidebar and the buttons instead of using Assembly.
{{</Note>}}

```html
<div class='absolute fl my24 mx24 py24 px24 bg-gray-faint round'>
  <form id='params'>
    <h4 class='txt-m txt-bold mb6'>Chose a travel mode:</h4>
    <div class='mb12 mr12 toggle-group align-center'>
      <label class='toggle-container'>
        <input name='profile' type='radio' value='walking'>
        <div class='toggle toggle--active-null toggle--null'>Walking</div>
      </label>
      <label class='toggle-container'>
        <input name='profile' type='radio' value='cycling' checked>
        <div class='toggle toggle--active-null toggle--null'>Cycling</div>
      </label>
      <label class='toggle-container'>
        <input name='profile' type='radio' value='driving'>
        <div class='toggle toggle--active-null toggle--null'>Driving</div>
      </label>
    </div>
    <h4 class='txt-m txt-bold mb6'>Chose a maximum duration:</h4>
    <div class='mb12 mr12 toggle-group align-center'>
      <label class='toggle-container'>
        <input name='duration' type='radio' value='10' checked>
        <div class='toggle toggle--active-null toggle--null'>10 min</div>
      </label>
      <label class='toggle-container'>
        <input name='duration' type='radio' value='20'>
        <div class='toggle toggle--active-null toggle--null'>20 min</div>
      </label>
      <label class='toggle-container'>
        <input name='duration' type='radio' value='30'>
        <div class='toggle toggle--active-null toggle--null'>30 min</div>
      </label>
  </form>
</div>
```

This code and the Assembly classes applied to it create a sidebar that contains toggle buttons that users will be able to select their desired mode of transportation (walking, cycling, or driving) and the amount of time to spend (10, 20, or 30 minutes).

Save your work and refresh the page. The sidebar will display on the left side of the page. While it looks good, clicking the buttons doesn't do anything &mdash; yet. In the next step, you will add a call to the Isochrone API, which you will be able to hook up to the user interface to create an interactive app.

{{
<AppropriateImage imageId="isochroneAddSidebar" alt="Screenshot showing a sidebar with buttons for driving profiles and trip durations" />
}}

## Add the Isochrone API

To integrate the Isochrone API into your app, you will write a new function, `getIso`, that will construct the query string and will use Ajax to make the Isochrone API call. Add the following code to your JavaScript, after the `map` variable that you used to initialize the map:

```js
// // Create variables to use in getIso()
var urlBase = 'https://api.mapbox.com/isochrone/v1/mapbox/';
var lon = -77.034;
var lat = 38.899;
var profile = 'cycling';
var minutes = 10;

// Create a function that sets up the Isochrone API query then makes an Ajax call
function getIso() {
  var query = urlBase + profile + '/' + lon + ',' + lat + '?contours_minutes=' + minutes + '&polygons=true&access_token=' + mapboxgl.accessToken;

  $.ajax({
    method: 'GET',
    url: query
  }).done(function(data) {
    console.log(data);
  })
};

// Call the getIso function
// You will remove this later - it's just here so you can see the console.log results in this step
getIso();
```

Since you have not set up the layers yet that will draw the isochrone contour described in the response to the map, this code prints the results of the query to the console. Save your work and refresh the page, and open your browser's developer tools panel. You will see the Isochrone API response object printed out to the console.

{{
<AppropriateImage imageId="isochroneConsoleLog" alt="Screenshot showing the results of the Isochrone API request logged to the console" />
}}

## Draw the isochrone contour

In the last step, you created a `console.log` statment to view the API response. But for this app, you want to show the isochrone contours on the map! To do this in Mapbox GL JS, you need to set up a new _source_ and a new _layer_. Learn more about the [`addSource`](https://docs.mapbox.com/mapbox-gl-js/api/#map#addsource) and [`addLayer`](https://docs.mapbox.com/mapbox-gl-js/api/#map#addlayer) methods in the Mapbox GL JS documentation.

Remove the `getIso();` call from the bottom of your JavaScript. Replace it with the following code:

```js
map.on('load', function() {
 // When the map loads, add the source and layer
 map.addSource('iso', {
   type: 'geojson',
   data: {
     'type': 'FeatureCollection',
     'features': []
   }
 });

 map.addLayer({
   'id': 'isoLayer',
   'type': 'fill',
   // Use "iso" as the data source for this layer
   'source': 'iso',
   'layout': {},
   'paint': {
     // The fill color for the layer is set to a light purple
     'fill-color': '#5a3fc0',
     'fill-opacity': 0.3
   }
 }, "poi-label");

 // Make the API call
 getIso();
});
```

Next, swap the `console.log(data)` statement in the `getIso` function with the following code, which will set the `iso` source to the data returned by the API call:

```js
// Set the 'iso' source's data to what's returned by the API query
map.getSource('iso').setData(data);
```

Save your changes and refresh the page in your browser. An isochrone contour for the hardcoded parameters (the `cycling` routing profile and a trip duration of 10 minutes) will be drawn to the map.

{{
<AppropriateImage imageId="isochroneDrawContour" alt="Screenshot showing the isochrone contour drawn on the map" />
}}

## Make the app interactive
Now, you need to hook the buttons that you created earlier up to your JavaScript so that users can change the routing profile and the trip duration and see the results displayed on the map. Add the following code to the bottom of your JavaScript, before the closing `</script>` tag:

```js
// Target the "params" form in the HTML portion of your code
var params = document.getElementById('params');

// When a user changes the value of profile or duration by clicking a button, change the parameter's value and make the API query again
params.addEventListener('change', function(e) {
  if (e.target.name === 'profile') {
    profile = e.target.value;
    getIso();
  } else if (e.target.name === 'duration') {
    minutes = e.target.value;
    getIso();
  }
});
```

Now, when you click the buttons to change the routing profile or the trip duration, the event listener sets the parameter in the query to the new value and runs the `getIso` function again. This in turn redraws the new isochrone contours to the map.

Save your changes and refresh the page in your browser. Click on different combinations of routing profiles and trip durations to see the isochrone contour change.

{{
<AppropriateImage imageId="isochroneChangeProfile" alt="Screenshot showing the isochrone contour has changed when the routing profile and duration buttons are used" />
}}

## Add a marker
As the last step, you will add a marker to your map at the coordinates of the query to make the center of the isochrone contour more distinct. In this case, the coordinates are set to the Mapbox office in Washington D.C.

Add the following code to your JavaScript, before the `map.on('load')` function:

```js
var marker = new mapboxgl.Marker({
 'color': '#314ccd'
});

// Create a LngLat object to use in the marker initialization
// https://docs.mapbox.com/mapbox-gl-js/api/#lnglat
var lngLat = {
 lon: lon,
 lat: lat
};
```

To draw the marker on the map when the map loads, add the following code inside of your `map.on('load')` function:
```js
// Initialize the marker at the query coordinates
marker.setLngLat(lngLat).addTo(map);
```

Now, when you save your work and refresh the page, you will see a blue marker at the specified coordinates.

{{
<AppropriateImage imageId="isochroneFinalProduct" alt="Screenshot showing a map with an isochrone contour and a marker at the query coordinates" />
}}

## Final product

You have created an app that uses the Mapbox Isochrone API to visualize how far a person could walk, bike, or drive within a given amount of time.

{{
 <DemoIframe src="/help/demos/get-started-isochrone-api/index2.html" />
}}

The final HTML file will look like the following:

```html
<!DOCTYPE html>
<html>

<head>
  <meta charset='utf-8' />
  <title>Get started with the Isochrone API</title>
  <meta name='viewport' content='initial-scale=1,maximum-scale=1,user-scalable=no' />
  <!-- Import Mapbox GL JS  -->
  <script src='https://api.tiles.mapbox.com/mapbox-gl-js/{{constants.VERSION_MAPBOXGLJS}}/mapbox-gl.js'></script>
  <link href='https://api.tiles.mapbox.com/mapbox-gl-js/{{constants.VERSION_MAPBOXGLJS}}/mapbox-gl.css' rel='stylesheet' />
  <!-- Import Assembly -->
  <link href='https://api.mapbox.com/mapbox-assembly/{{constants.ASSEMBLY}}/assembly.min.css' rel='stylesheet'>
  <script src='https://api.mapbox.com/mapbox-assembly/{{constants.ASSEMBLY}}/assembly.js'> </script>
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
  <!-- Create a container for the map -->
  <div id='map'></div>

  <!-- Create a sidebar with buttons for each option -->
  <div class='absolute fl my24 mx24 py24 px24 bg-gray-faint round'>
    <form id='params'>
      <h4 class='txt-m txt-bold mb6'>Chose a travel mode:</h4>
      <div class='mb12 mr12 toggle-group align-center'>
        <label class='toggle-container'>
          <input name='profile' type='radio' value='walking'>
          <div class='toggle toggle--active-null toggle--null'>Walking</div>
        </label>
        <label class='toggle-container'>
          <input name='profile' type='radio' value='cycling' checked>
          <div class='toggle toggle--active-null toggle--null'>Cycling</div>
        </label>
        <label class='toggle-container'>
          <input name='profile' type='radio' value='driving'>
          <div class='toggle toggle--active-null toggle--null'>Driving</div>
        </label>
      </div>
      <h4 class='txt-m txt-bold mb6'>Chose a maximum duration:</h4>
      <div class='mb12 mr12 toggle-group align-center'>
        <label class='toggle-container'>
          <input name='duration' type='radio' value='10' checked>
          <div class='toggle toggle--active-null toggle--null'>10 min</div>
        </label>
        <label class='toggle-container'>
          <input name='duration' type='radio' value='20'>
          <div class='toggle toggle--active-null toggle--null'>20 min</div>
        </label>
        <label class='toggle-container'>
          <input name='duration' type='radio' value='30'>
          <div class='toggle toggle--active-null toggle--null'>30 min</div>
        </label>
    </form>
  </div>

  <script>
    // Add your Mapbox access token
    mapboxgl.accessToken = '{{ <UserAccessToken /> }}';
    var map = new mapboxgl.Map({
      container: 'map', // Specify the container ID
      style: 'mapbox://styles/mapbox/streets-v{{constants.VERSION_STREETS_STYLE}}', // Specify which map style to use
      center: [-77.0369, 38.895], // Specify the starting position
      zoom: 11.5, // Specify the starting zoom
    });

    // Create variables to use in getIso()
    var urlBase = 'https://api.mapbox.com/isochrone/v1/mapbox/';
    var lon = -77.034;
    var lat = 38.899;
    var profile = 'cycling';
    var minutes = 10;

    // Create a function that sets up the Isochrone API query then makes an Ajax call
    function getIso() {
      var query = urlBase + profile + '/' + lon + ',' + lat + '?contours_minutes=' + minutes + '&polygons=true&access_token=' + mapboxgl.accessToken;

      $.ajax({
        method: 'GET',
        url: query
      }).done(function(data) {
        // Set the 'iso' source's data to what's returned by the API query
        map.getSource('iso').setData(data);
      })
    };

    var marker = new mapboxgl.Marker({
      'color': '#314ccd'
    });

    // Create a LngLat object to use in the marker initialization
    // https://docs.mapbox.com/mapbox-gl-js/api/#lnglat
    var lngLat = {
      lon: lon,
      lat: lat
    };

    map.on('load', function() {
      // When the map loads, add the source and layer
      map.addSource('iso', {
        type: 'geojson',
        data: {
          "type": 'FeatureCollection',
          "features": []
        }
      });

      map.addLayer({
        'id': 'isoLayer',
        'type': 'fill',
        // Use "iso" as the data source for this layer
        'source': 'iso',
        'layout': {},
        'paint': {
          // The fill color for the layer is set to a light purple
          'fill-color': '#5a3fc0',
          'fill-opacity': 0.3
        }
      }, "poi-label");

      // Initialize the marker at the query coordinates
      marker.setLngLat(lngLat).addTo(map);

      // Make the API call
      getIso();
    });

    // Target the "params" form in the HTML portion of your code
    var params = document.getElementById('params');

    // When a user changes the value of profile or duration by clicking a button, change the parameter's value and make the API query again
    params.addEventListener('change', function(e) {
      if (e.target.name === 'profile') {
        profile = e.target.value;
        getIso();
      } else if (e.target.name === 'duration') {
        minutes = e.target.value;
        getIso();
      }
    });
  </script>
</body>

</html>
```

## Next steps

To build on top of the tools and techniques you used in this tutorial, explore the following resources:
- Learn more about how you can use the Isochrone API's optional parameters to influence what gets returned in the response object in the [Isochrone API documentation](https://docs.mapbox.com/api/navigation/#isochrone).
- Learn more about adding layers to a map using Mapbox GL JS in the [Add a GeoJSON line example](https://docs.mapbox.com/mapbox-gl-js/example/geojson-line/) and in the [`addLayer` documentation](https://docs.mapbox.com/mapbox-gl-js/api/#map#addlayer).
