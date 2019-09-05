---
title: Get started with the Map Matching API
description: Create a web app that uses the Mapbox Map Matching API to allow users to specify their own driving route.
thumbnail: mapMatchingGetStartedDirections
topics:
- navigation
- directions
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
  - "import { ColorSwatch } from '../../components/color-swatch';"
contentType: tutorial
---

Most turn-by-turn apps assume that users want to take the most efficient route to their destination. But sometimes, users care more about being able to choose a fun or scenic route than they do about getting to their destination quickly. For example: _Your user is visiting San Francisco. They visited the Maritime Museum, and now it’s time to get a slice of pizza in North Beach. On the way, they want to drive down Lombard Street, a stretch of road with eight tight hairpin turns that’s popularly known as the “crookedest street in the world”._

Taking Lombard Street isn't the fastest way to get to the user’s destination, but it does offer more photo opportunities than any other route! In most turn-by-turn apps, it’s difficult to pull up a route that includes this stretch of Lombard Street because it’s not the most efficient route. This means a user would be routed elsewhere, regardless of their wish to drive down Lombard Street. But the [Mapbox Map Matching API](https://docs.mapbox.com/api/navigation/#map-matching) makes it possible to plot custom routes, which opens up different routing possibilities.

In this tutorial, you will create a web application that allows your users to create their own travel routes, regardless of whether those routes are the most efficient routes or not. The app's users will draw their own route on the map using draw tools from the **Mapbox GL Draw plugin**, then the app will pass the drawn coordinates to the **Map Matching API** and generate turn-by-turn directions for the new driving route.

{{
  <DemoIframe src="/help/demos/get-started-map-matching-api/index.html" />
}}

{{<Note title="The Map Matching API vs. the Directions API" imageComponent={<BookImage />}>}}

The Mapbox Map Matching API has a lot of similarities to the [Directions API](https://docs.mapbox.com/api/navigation/#directions). The Map Matching API can be used to generate routes, route durations, and turn-by-turn directions, as the Directions API can. But the Directions API will specifically always generate an _optimal_ route, while the Map Matching API will generate a route on the OpenStreetMap road network that most closely follows the coordinates provided in the request.

{{</Note>}}

## Getting started
To complete this tutorial, you will need:

- **A Mapbox access token.** Your Mapbox access tokens are on your [Account page](https://account.mapbox.com/).
- **Mapbox GL JS.** [Mapbox GL JS](https://docs.mapbox.com/mapbox-gl-js/overview/) is a JavaScript API for building web maps.
- **Mapbox GL Draw plugin.** The [Mapbox GL Draw plugin](https://github.com/mapbox/mapbox-gl-draw) adds support for drawing and editing features on maps created with Mapbox GL JS.
- **Mapbox Map Matching API.** The [Map Matching API](https://docs.mapbox.com/api/navigation/#map-matching) snaps coordinates onto the OpenStreetMap road network, and can return turn-by-turn directions for the routes it produces.   
- **jQuery.** [jQuery](https://jquery.com/) is a JavaScript library you will use to add your API request to your application.
- **A text editor.** Use the text editor of your choice for writing HTML, CSS, and JavaScript.

## Create a map
To start the app, you will create a map using [Mapbox GL JS](https://docs.mapbox.com/mapbox-gl-js/api/).

Open your text editor and create a new file named `index.html`. Set up this new HTML file by pasting the following code into your text editor. This code creates the structure of the page. This code also imports Mapbox GL JS and jQuery in the `<head>` of the page. The Mapbox GL JS JavaScript and CSS files allow you to use Mapbox GL JS functionality and style, while jQuery will allow you to use [Ajax](https://api.jquery.com/jquery.ajax/) to parse your Map Matching API call.

There is a `<div>` element with the ID `map` in the `<body>` of the page. This `<div>` is the container in which the map will be displayed on the page.

```html
<!DOCTYPE html>
<html>

<head>
  <meta charset='utf-8' />
  <title>Get started with the Map Matching API</title>
  <meta name='viewport' content='initial-scale=1,maximum-scale=1,user-scalable=no' />
  <!-- Import Mapbox GL JS  -->
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
  <!-- Create a container for the map -->
  <div id='map'></div>

  <script>
    // Add your Mapbox access token
    mapboxgl.accessToken = '{{ <UserAccessToken /> }}';
    var map = new mapboxgl.Map({
      container: 'map', // Specify the container ID
      style: 'mapbox://styles/mapbox/streets-v{{constants.VERSION_STREETS_STYLE}}', // Specify which map style to use
      center: [-122.42136449,37.80176523], // Specify the starting position
      zoom: 14.5, // Specify the starting zoom
    });
  </script>
</body>

</html>
```

This Mapbox GL JS code sets a style for the map, gives it coordinates on which to center, and sets a zoom level.

Save your changes. Open the HTML file in your browser to see the rendered map, which is centered on the city of San Francisco.

## Add the Draw tools

{{<Note title="Options for passing coordinates to the Map Matching API" imageComponent={<BookImage />}>}}

In this app created in this tutorial, the coordinates that the Map Matching API uses to generate a route are created by the user adding points directly to the map with the Mapbox GL Draw tools. Often, though, you would instead want to add the points used by the Map Matching API programmatically. For example, the Map Matching API could access a data set that contains landmark coordinates to create scenic routes, or a data set with the locations of known parking garages near the end of a route.

{{</Note>}}

The [Mapbox GL Draw plugin](https://github.com/mapbox/mapbox-gl-draw) adds support for drawing features on maps created with Mapbox GL JS. In this step, you will add the Mapbox GL Draw `line_tool` and `trash` tools to your app, which will allow your users to draw lines and delete them. To add the draw tools, first add the links to the Mapbox GL Draw plugin's JavaScript and CSS to the head of the HTML file:

```html
<script src='https://api.mapbox.com/mapbox-gl-js/plugins/mapbox-gl-draw/v1.0.9/mapbox-gl-draw.js'></script>
<link rel='stylesheet' href='https://api.mapbox.com/mapbox-gl-js/plugins/mapbox-gl-draw/v1.0.9/mapbox-gl-draw.css' type='text/css' />
```

Once these links have been added, you will be able to use the Draw plugin in your app. When you add the Draw plugin, you can also specify the style of the line that gets drawn on the map when a user uses the draw tool. Add the following code above the closing `</script>` tag in your HTML file.

```js
var draw = new MapboxDraw({
  // Instead of showing all the draw tools, show only the line string and delete tools
  displayControlsDefault: false,
  controls: {
    line_string: true,
    trash: true
  },
  styles: [
    // Set the line style for the user-input coordinates
    {
      "id": "gl-draw-line",
      "type": "line",
      "filter": ["all", ["==", "$type", "LineString"],
        ["!=", "mode", "static"]
      ],
      "layout": {
        "line-cap": "round",
        "line-join": "round"
      },
      "paint": {
        "line-color": "#438EE4",
        "line-dasharray": [0.2, 2],
        "line-width": 4,
        "line-opacity": 0.7
      }
    },
    // Style the vertex point halos
    {
      "id": "gl-draw-polygon-and-line-vertex-halo-active",
      "type": "circle",
      "filter": ["all", ["==", "meta", "vertex"],
        ["==", "$type", "Point"],
        ["!=", "mode", "static"]
      ],
      "paint": {
        "circle-radius": 12,
        "circle-color": "#FFF"
      }
    },
    // Style the vertex points
    {
      "id": "gl-draw-polygon-and-line-vertex-active",
      "type": "circle",
      "filter": ["all", ["==", "meta", "vertex"],
        ["==", "$type", "Point"],
        ["!=", "mode", "static"]
      ],
      "paint": {
        "circle-radius": 8,
        "circle-color": "#438EE4",
      }
    },
  ]
});

// Add the draw tool to the map
map.addControl(draw);
```

Save your file, then refresh the page in your browser. You will see icons for the specified Draw plugin controls, `line_tool` and `delete`, on the upper right side of the page. Click the `line_tool` icon. On the map, click once to start the line, then click one or more times to draw a path. When you're done drawing, click again on the last point to finish the path. The map will display a blue dashed line that follows the path you drew. For more information on how to style lines using this plugin, read the [Styling Draw section](https://github.com/mapbox/mapbox-gl-draw/blob/master/docs/API.md#styling-draw) of the Mapbox GL Draw documentation.

In a few steps, you will link the code you wrote in this step with a function that takes this drawn path and gathers the coordinates to use in the Map Matching API call.  

{{
<AppropriateImage imageId="mapMatchingGetStartedDrawTools" alt="Screenshot showing the Mapbox GL Draw plugin tools added to the right side of the map." />
}}

## Add the sidebar

Next, add a sidebar to the web app that will display instructions for users on how to use the app. This sidebar will also serve as a place to display turn-by-turn directions, which you will set up in a later step.

In the `<body>` of your HTML, add a new `<div>`. This `<div>` will hold the app's instructions and, later, the directions.

```html
<div class="info-box">
  <div id="info">
    <p>Draw your route using the draw tools on the right. To get the most accurate route match, draw points at regular intervals.</p>
  </div>
  <div id="directions"></div>
</div>
```

To style the new `<div>`, add the following CSS to the `<style>` section of your HTML:

```css
.info-box {
  position: absolute;
  margin: 20px;
  width: 25%;
  top: 0;
  bottom: 40%;
  padding: 20px;
  background-color: rgba(255, 255, 255, 0.9);
  overflow-y: scroll;
  font-family: sans-serif;
  font-size: 0.8em;
  line-height: 2em;
}

#info {
  font-size: 16px;
  font-weight: bold;
}
```

Save your work and refresh the page. The new information box will display on the left side of the page.

{{
<AppropriateImage imageId="mapMatchingGetStartedSidebar" alt="Screenshot showing a sidebar added to the map." />
}}

## Add the Map Matching API

A Map Matching API requires two parameters: the `profile` the query should use, and the `coordinates` that need to be matched to the OpenStreetMap road and path network. The `profile` can be either `walking`, `cycling`, `driving`, or `driving-traffic`. The `coordinates` are a semicolon-separated list of `{longitude},{latitude}` coordinate pairs to visit in order, of which there can be anywhere between two and 100.

```
https://api.mapbox.com/matching/v5/mapbox/{profile}/{coordinates}.json?access_token=YOUR_MAPBOX_ACCESS_TOKEN
```

The Map Matching API also accepts several optional parameters that can be used to customize the query. For this app, you will be using two optional parameters:

- `radiuses`: A semicolon-separated list that indicates the maximum distance a coordinate can be moved to snap to the road network in meters. Adding a radius tells the Map Matching API how precisely it must match the input coordinates, which may not always represent a location on the OpenStreetMap road network. The number of radiuses must be the same as the number of coordinates in the request.
- `steps`: Set to `true` to return step-by-step instructions.

To learn more about the Map Matching API and its other optional parameters, explore the [Map Matching API documentation](https://docs.mapbox.com/api/navigation/#map-matching).

This example query uses the `driving` profile, has two coordinate pairs and two `radiuses`, and has the `steps` parameter set to `true`:

```
https://api.mapbox.com/matching/v5/mapbox/driving/-117.17282,32.71204;-117.17288,32.71225?steps=true&radiuses=25;25&access_token={{ <UserAccessToken /> }}
```

A Map Matching API request that includes the `radiuses` and `steps` parameters returns a response that contains `matchings`, an array of match objects. A match object contains route leg objects, which give detailed information about each leg of the route, including the turn-by-turn directions. You will use the information returned by the Map Matching API to do two things: draw the matched route to the map, and return turn-by-turn directions.

To integrate the Map Matching API into your app, you will write two new functions, `updateRoute` and `getMatch`. `updateRoute` will take the coordinates from the user-generated line and format them so that they can be used in a Map Matching query. `getMatch` will construct the query string and will use Ajax to make the Map Matching API call. Used together, these two functions will make an API call using the coordinates drawn on the screen and will return the data necessary to complete the rest of the app. Add the following code to your JavaScript, before the closing `</script>` tag:

```js
// Use the coordinates you drew to make the Map Matching API request
function updateRoute() {
  // Set the profile
  var profile = "driving";
  // Get the coordinates that were drawn on the map
  var data = draw.getAll();
  var lastFeature = data.features.length - 1;
  var coords = data.features[lastFeature].geometry.coordinates;
  // Format the coordinates
  var newCoords = coords.join(';')
  // Set the radius for each coordinate pair to 25 meters
  var radius = [];
  coords.forEach(element => {
    radius.push(25);
  });
  getMatch(newCoords, radius, profile);
}

// Make a Map Matching request
function getMatch(coordinates, radius, profile) {
  // Separate the radiuses with semicolons
  var radiuses = radius.join(';')
  // Create the query
  var query = 'https://api.mapbox.com/matching/v5/mapbox/' + profile + '/' + coordinates + '?geometries=geojson&radiuses=' + radiuses + '&steps=true&access_token=' + mapboxgl.accessToken;

  $.ajax({
    method: 'GET',
    url: query
  }).done(function(data) {
    // Get the coordinates from the response
    var coords = data.matchings[0].geometry;
    console.log(coords);
    // Code from the next step will go here
  });
}
```

By calling the `getMatch` function in `updateRoute`, you can access the user-drawn coordinates and use them as the coordinates in the Map Matching API call. In the next step you will add a new drawn line to show the matched route, but for now you can view the coordinate results using `console.log()`.

To call `getMatch` when your user draws or updates a line on the map, add the following lines before the closing `</script>` tag:

```js
map.on('draw.create', updateRoute);
map.on('draw.update', updateRoute);
```

Save your work, then refresh your browser page and open the browser's developer tools. When you draw a route on the map, your app will print the coordinate data returned by the Map Matching API to the JavaScript console.

{{
<AppropriateImage imageId="mapMatchingGetStartedConsole" alt="Screenshot showing the returned coordinates displayed in a browser's JavaScript console." />
}}

## Draw the Map Matching route
Next, you will create an `addRoute` function that takes the coordinates returned by the Map Matching API and adds them on the map as a new layer. Paste the following code into your JavaScript, above the final `</script>` tag:

```js
// Draw the Map Matching route as a new layer on the map
function addRoute(coords) {
  // If a route is already loaded, remove it
  if (map.getSource('route')) {
    map.removeLayer('route')
    map.removeSource('route')
  } else { // Add a new layer to the map
    map.addLayer({
      "id": "route",
      "type": "line",
      "source": {
        "type": "geojson",
        "data": {
          "type": "Feature",
          "properties": {},
          "geometry": coords
        }
      },
      "layout": {
        "line-join": "round",
        "line-cap": "round"
      },
      "paint": {
        "line-color": "#03AA46",
        "line-width": 8,
        "line-opacity": 0.8
      }
    });
  };
}
```

Call `addRoute` within your `getRoute` function so that it can access the coordinates returned by the Map Matching API. `getRoute` will now look like this:

```js
// Make a Map Matching request
function getMatch(coordinates, radius, profile) {
  // Separate the radiuses with semicolons
  var radiuses = radius.join(';')
  // Create the query
  var query = 'https://api.mapbox.com/matching/v5/mapbox/' + profile + '/' + coordinates + '?geometries=geojson&radiuses=' + radiuses + '&steps=true&access_token=' + mapboxgl.accessToken;
  console.log(query)
  $.ajax({
    method: 'GET',
    url: query
  }).done(function(data) {
    // Get the coordinates from the response
    var coords = data.matchings[0].geometry;
    // Draw the route on the map
    addRoute(coords);
  });
}
```

Save your changes and refresh the browser page. Now when you use the `line_draw` tool to trace a route, the route generated by the Map Matching API also shows on the map. As you can see, the line drawn by the user won't always match up directly with the route generated by the Map Matching API. This is because the Map Matching API takes the input coordinates, which may not be located directly on the road network, and snaps them to the nearest road within the 25 meter radius that you specified in the `radiuses` parameter.

{{
<AppropriateImage imageId="mapMatchingGetStartedNewLayer" alt="Screenshot showing the coordinates returned by the Map Matching API as a new layer on the map." />
}}

## Display the turn-by-turn directions
Now it's time to add the turn-by-turn instructions from the Map Matching API to the sidebar! Doing so requires writing a new function, `getInstructions`, that will allow you to dig down into the Map Matching API response object to get the information you need: the total time that the route will take, and the maneuver instructions for each step of the route. (Read more about what gets returned in the Map Matching API's route step object in the [Map Matching API documentation](https://docs.mapbox.com/api/navigation/#route-step-object).) Add the following code to the JavaScript, below the `getMatch` method:

```js
function getInstructions(data) {
  // Target the sidebar to add the instructions
  var directions = document.getElementById('directions');

  var legs = data.legs;
  var tripDirections = [];
  // Output the instructions for each step of each leg in the response object
  for (var i = 0; i < legs.length; i++) {
    var steps = legs[i].steps;
    for (var j = 0; j < steps.length; j++) {
      tripDirections.push('<br><li>' + steps[j].maneuver.instruction) + '</li>';
    }
  }
  directions.innerHTML = '<br><h2>Trip duration: ' + Math.floor(data.duration / 60) + ' min.</h2>' + tripDirections;
}
```

Next, call `getInstructions` within your `getRoute` function so that it can access the data returned by the Map Matching API. `getRoute` will now look like this:

```js
// Make a Map Matching request
function getMatch(coordinates, radius, profile) {
  // Separate the radiuses with semicolons
  var radiuses = radius.join(';')
  // Create the query
  var query = 'https://api.mapbox.com/matching/v5/mapbox/' + profile + '/' + coordinates + '?geometries=geojson&radiuses=' + radiuses + '&steps=true&access_token=' + mapboxgl.accessToken;
  console.log(query)
  $.ajax({
    method: 'GET',
    url: query
  }).done(function(data) {
    var coords = data.matchings[0].geometry;
    // Draw the route on the map
    addRoute(coords);
    getInstructions(data.matchings[0]);
  });
}
```

Save your changes and refresh your browser page. Now when you draw a route on the map, you will see the trip duration and the turn-by-turn instructions in the sidebar.

{{
<AppropriateImage imageId="mapMatchingGetStartedDirections" alt="Screenshot showing turn-by-turn directions displayed in the sidebar of the map." />
}}

## Let users delete a route
The last step is to add a function that allows your users to delete a route they have drawn on the map.

```js
// If the user clicks the delete draw button, remove the layer if it exists
function removeRoute() {
  if (map.getSource('route')) {
    map.removeLayer('route');
    map.removeSource('route');
  } else {
    return;
  }
}
```

To connect the `removeRoute` function with the Mapbox GL Draw plugin's delete button, add the following line to your JavaScript:

```js
  map.on('draw.delete', removeRoute);
```

Save your work and refresh the browser page. When you draw a line and then click the Draw plugin's delete button, the line is removed from the page.

## Final product

You have created an app that uses the Mapbox Map Matching API to snap user-provided coordinates to the road network, while at the same time displaying the route on a map and showing users the turn-by-turn instructions for the route.  

{{
  <DemoIframe src="/help/demos/get-started-map-matching-api/index.html" />
}}

The final HTML file will look like the following:

```html
<!DOCTYPE html>
<html>

<head>
  <meta charset='utf-8' />
  <title>Get started with the Map Matching API</title>
  <meta name='viewport' content='initial-scale=1,maximum-scale=1,user-scalable=no' />
  <!-- Import Mapbox GL JS  -->
  <script src='https://api.tiles.mapbox.com/mapbox-gl-js/{{constants.VERSION_MAPBOXGLJS}}/mapbox-gl.js'></script>
  <link href='https://api.tiles.mapbox.com/mapbox-gl-js/{{constants.VERSION_MAPBOXGLJS}}/mapbox-gl.css' rel='stylesheet' />
  <!-- Import jQuery -->
  <script src='https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js'></script>
  <!-- Import Mapbox GL Draw -->
  <script src='https://api.mapbox.com/mapbox-gl-js/plugins/mapbox-gl-draw/v1.0.9/mapbox-gl-draw.js'></script>
  <link rel='stylesheet' href='https://api.mapbox.com/mapbox-gl-js/plugins/mapbox-gl-draw/v1.0.9/mapbox-gl-draw.css' type='text/css' />

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

    .info-box {
      position: absolute;
      margin: 20px;
      width: 25%;
      top: 0;
      bottom: 40%;
      padding: 20px;
      background-color: rgba(255, 255, 255, 0.9);
      overflow-y: scroll;
      font-family: sans-serif;
      font-size: 0.8em;
      line-height: 2em;
    }

    #info {
      font-size: 16px;
      font-weight: bold;
    }
  </style>
</head>

<body>
  <!-- Create a container for the map -->
  <div id='map'></div>

  <div class="info-box">
    <div id="info">
      <p>Draw your route using the draw tools on the right. To get the most accurate route match, draw points at regular intervals.</p>
    </div>
    <div id="directions"></div>
  </div>

  <script>
    // Add your Mapbox access token
    mapboxgl.accessToken = '{{ <UserAccessToken/> }}';
    var map = new mapboxgl.Map({
      container: 'map', // Specify the container ID
      style: 'mapbox://styles/mapbox/streets-v{{constants.VERSION_STREETS_STYLE}}', // Specify which map style to use
      center: [-122.42136449,37.80176523], // Specify the starting position
      zoom: 14.5, // Specify the starting zoom
    });

    var draw = new MapboxDraw({
      // Instead of showing all the draw tools, show only the line string and delete tools
      displayControlsDefault: false,
      controls: {
        line_string: true,
        trash: true
      },
      styles: [
        // Set the line style for the user-input coordinates
        {
          "id": "gl-draw-line",
          "type": "line",
          "filter": ["all", ["==", "$type", "LineString"],
            ["!=", "mode", "static"]
          ],
          "layout": {
            "line-cap": "round",
            "line-join": "round"
          },
          "paint": {
            "line-color": "#438EE4",
            "line-dasharray": [0.2, 2],
            "line-width": 4,
            "line-opacity": 0.7
          }
        },
        // Style the vertex point halos
        {
          "id": "gl-draw-polygon-and-line-vertex-halo-active",
          "type": "circle",
          "filter": ["all", ["==", "meta", "vertex"],
            ["==", "$type", "Point"],
            ["!=", "mode", "static"]
          ],
          "paint": {
            "circle-radius": 12,
            "circle-color": "#FFF"
          }
        },
        // Style the vertex points
        {
          "id": "gl-draw-polygon-and-line-vertex-active",
          "type": "circle",
          "filter": ["all", ["==", "meta", "vertex"],
            ["==", "$type", "Point"],
            ["!=", "mode", "static"]
          ],
          "paint": {
            "circle-radius": 8,
            "circle-color": "#438EE4",
          }
        },
      ]
    });

    // Add the draw tool to the map
    map.addControl(draw);

    function updateRoute() {
      // Set the profile
      var profile = "driving";
      // Get the coordinates that were drawn on the map
      var data = draw.getAll();
      var lastFeature = data.features.length - 1;
      var coords = data.features[lastFeature].geometry.coordinates;
      // Format the coordinates
      var newCoords = coords.join(';')
      // Set the radius for each coordinate pair to 25 meters
      var radius = [];
      coords.forEach(element => {
        radius.push(25);
      });
      getMatch(newCoords, radius, profile);
    }

    // Make a Map Matching request
    function getMatch(coordinates, radius, profile) {
      // Separate the radiuses with semicolons
      var radiuses = radius.join(';')
      // Create the query
      var query = 'https://api.mapbox.com/matching/v5/mapbox/' + profile + '/' + coordinates + '?geometries=geojson&radiuses=' + radiuses + '&steps=true&access_token=' + mapboxgl.accessToken;

      $.ajax({
        method: 'GET',
        url: query
      }).done(function(data) {
        // Get the coordinates from the response
        var coords = data.matchings[0].geometry;
        // Draw the route on the map
        addRoute(coords);
        getInstructions(data.matchings[0]);
      });
    }

    // Draw the Map Matching route as a new layer on the map
    function addRoute(coords) {
      // If a route is already loaded, remove it
      if (map.getSource('route')) {
        map.removeLayer('route')
        map.removeSource('route')
      } else {
        map.addLayer({
          "id": "route",
          "type": "line",
          "source": {
            "type": "geojson",
            "data": {
              "type": "Feature",
              "properties": {},
              "geometry": coords
            }
          },
          "layout": {
            "line-join": "round",
            "line-cap": "round"
          },
          "paint": {
            "line-color": "#03AA46",
            "line-width": 8,
            "line-opacity": 0.8
          }
        });
      };
    }

    function getInstructions(data) {
      // Target the sidebar to add the instructions
      var directions = document.getElementById('directions');

      var legs = data.legs;
      var tripDirections = [];
      // Output the instructions for each step of each leg in the response object
      for (var i = 0; i < legs.length; i++) {
        var steps = legs[i].steps;
        for (var j = 0; j < steps.length; j++) {
          tripDirections.push('<br><li>' + steps[j].maneuver.instruction) + '</li>';
        }
      }
      directions.innerHTML = '<br><h2>Trip duration: ' + Math.floor(data.duration / 60) + ' min.</h2>' + tripDirections;
    }

    // If the user clicks the delete draw button, remove the layer if it exists
    function removeRoute() {
      if (map.getSource('route')) {
        map.removeLayer('route');
        map.removeSource('route');
      } else {
        return;
      }
    }

    map.on('draw.create', updateRoute);
    map.on('draw.update', updateRoute);
    map.on('draw.delete', removeRoute);
  </script>
</body>

</html>

```

## Next steps
To build on top of the tools and techniques you used in this tutorial, explore the following resources:
- Learn more about how you can use the Map Matching API's optional parameters to influence what gets returned in the response object in the [Map Matching API documentation](https://docs.mapbox.com/api/navigation/#map-matching).
- Learn more about adding layers to a map using Mapbox GL JS in the [Add a GeoJSON line example](https://docs.mapbox.com/mapbox-gl-js/example/geojson-line/) and in the [`addLayer` documentation](https://docs.mapbox.com/mapbox-gl-js/api/#map#addlayer).
- Learn more about how to use the Mapbox GL Draw plugin in the [Show drawn polygon area example](https://docs.mapbox.com/mapbox-gl-js/example/mapbox-gl-draw/) and in the [Mapbox GL Draw plugin documentation](https://github.com/mapbox/mapbox-gl-draw/tree/master/docs).
