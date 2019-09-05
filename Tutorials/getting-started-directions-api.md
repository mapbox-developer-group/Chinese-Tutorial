---
title: Getting started with the Mapbox Directions API
description: Add routing capabilities to your application with the Mapbox Directions API.
thumbnail: directionsApi
level: 1
language:
- JavaScript
topics:
- directions
prependJs:
  - "import * as constants from '../../constants';"
  - "import Note from '@mapbox/dr-ui/note';"
  - "import BookImage from '@mapbox/dr-ui/book-image';"
  - "import UserAccessToken from '../../components/user-access-token';"
  - "import DemoIframe from '@mapbox/dr-ui/demo-iframe';"
contentType: tutorial
---

The [Mapbox Directions API](https://docs.mapbox.com/api/navigation/#directions) makes it possible to provide users with routes, turn instructions, and trip durations. This tutorial walks you through the process of requesting directions, adding a single bike route between a fixed location and a clicked location, and displaying the route's turn-by-turn instructions.

{{
  <DemoIframe src="/help/demos/directions-api/index.html" />
}}

## Getting started

Here are a few resources you'll need before getting started:

- [**An access token**](/help/glossary/access-token/) from your account. You will use an access token to associate a map with your account and you can find it on the  [Account page](https://www.mapbox.com/account/).
- [**Mapbox Directions API documentation**](https://docs.mapbox.com/api/navigation/#directions). A reference for all options available when making requests and how to interpret responses.
- [__Mapbox GL JS__](https://docs.mapbox.com/mapbox-gl-js/overview/). The Mapbox JavaScript library that uses WebGL to render interactive maps from Mapbox GL styles.
- __A text editor.__ You'll be writing HTML, CSS, and JavaScript.

## Build a Directions API request

When making a request to any Mapbox web service, the general structure of the request URL will start like this:

```
https://api.mapbox.com/{service}/
```

In this case, the `{service}` will be `directions`, but you can also make requests of `styles`, `geocoding`, and other Mapbox APIs.

The next part will be the version number. The version number is helpful to know since the API may change over time and provide you with greater capabilities or change how the requests may work. The current version for directions is `v5`:

```
https://api.mapbox.com/directions/v5/
```

### Parameters

If you tried to paste this into your browser's address bar, the request would not return anything. You still need to pass in some parameters that will narrow the scope of your request. In the case of the Mapbox Directions API, you are required to supply a **profile** (a mode of travel) and **coordinates** (the origin and the destination) for your request:

- In this case, use the `cycling` profile to generate a bike route.
- Use `-84.518641, 39.134270` as your starting coordinate and `-84.512023, 39.102779` as your destination. Note that these coordinates must be separated by a semi-colon `;`.
- Use the optional parameter `geometries=geojson` to specify that you would like it to return the route as a GeoJSON feature.

```
https://api.mapbox.com/directions/v5/mapbox/cycling/-84.518641,39.134270;-84.512023,39.102779?geometries=geojson
```

### Access token

The only required item left is your access token. The access token is required to track the requests you make from your account _for this particular service_. You can create specific tokens for your requests or use your default token.

When adding this token, use an ampersand (the `&` symbol) before the token to append this to the request:

```
https://api.mapbox.com/directions/v5/mapbox/cycling/-84.518641,39.134270;-84.512023,39.102779?geometries=geojson&access_token={{ <UserAccessToken /> }}
```

Now that you have a request, paste the full URL into your browser's address bar to get a response.

## Review the response

When you make your request, a JSON object will be returned with the following information:

- **waypoints**: This is an array of _Waypoint_ objects. In this case, this array will include your starting and ending points.
- **routes**: This is an array of _Route_ objects ordered by descending recommendation rank. In this case, you have not requested alternative routes, so only one route will be returned. You will use the `geometry` property to display the route on a map in the next step.
- **code**: This string indicates the state of the response. On normal valid responses, the value will be `Ok`.

```json
{
  "waypoints": [
    {
      "location": [
        -84.518399,
        39.134126
      ],
      "name": ""
    },
    {
      "location": [
        -84.511987,
        39.102638
      ],
      "name": "East 6th Street"
    }
  ],
  "routes": [
    {
      "legs": [
        {
          "steps": [],
          "weight": 1332.6,
          "distance": 4205,
          "summary": "",
          "duration": 1126
        }
      ],
      "weight_name": "cyclability",
      "geometry": {
        "coordinates": [
          [
            -84.518399,
            39.134126
          ],
          [
            -84.51841,
            39.133781
          ],
          [
            -84.520024,
            39.133456
          ],
          [
            -84.520321,
            39.132597
          ],
          [
            -84.52085,
            39.128019
          ],
          [
            -84.52036,
            39.127901
          ],
          [
            -84.52094,
            39.122783
          ],
          [
            -84.52022,
            39.122713
          ],
          [
            -84.520768,
            39.120841
          ],
          [
            -84.519639,
            39.120268
          ],
          [
            -84.51233,
            39.114141
          ],
          [
            -84.512652,
            39.11311
          ],
          [
            -84.512399,
            39.112216
          ],
          [
            -84.513232,
            39.112084
          ],
          [
            -84.512127,
            39.107599
          ],
          [
            -84.512904,
            39.107489
          ],
          [
            -84.511692,
            39.102682
          ],
          [
            -84.511987,
            39.102638
          ]
        ],
        "type": "LineString"
      },
      "weight": 1332.6,
      "distance": 4205,
      "duration": 1126
    }
  ],
  "code": "Ok"
}
```

## Build the map

Now that you understand how Mapbox Directions API requests and responses both work, you can use this API request to add a route to a web map.

### Set up your HTML file

Create a new HTML file called `index.html` and initialize a Mapbox GL JS map using the code below.

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset='utf-8' />
    <title></title>
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
    // add the JavaScript here
    </script>
  </body>
</html>
```

Next, add the following script to the block of code within the `<script>` tags to initialize your map, the style, and starting position:

```js
mapboxgl.accessToken = '{{ <UserAccessToken /> }}';
var map = new mapboxgl.Map({
  container: 'map',
  style: 'mapbox://styles/mapbox/streets-v10',
  center: [-122.662323, 45.523751], // starting position
  zoom: 12
});
// set the bounds of the map
var bounds = [[-123.069003, 45.395273], [-122.303707, 45.612333]];
map.setMaxBounds(bounds);

// initialize the map canvas to interact with later
var canvas = map.getCanvasContainer();

// an arbitrary start will always be the same
// only the end or destination will change
var start = [-122.662323, 45.523751];

// this is where the code for the next step will go
```


### Add your route request function

Next, you'll build a function called `getRoute` to make the API request and add the resulting route as a new layer. You'll then call that function when the map loads.

Within the `getRoute` function, specify the `start` and `end` coordinates. The start was defined outside of this function and the end will be passed in as an argument. Use an [XHR](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest) object to make the API request. You can then use the response to get all the relevant objects and use the geometry to add the response as a layer to the map. You can end this part of the code by executing it with a request _after_ the map loads so that it makes a route that begins and ends at the start location.

Add the following code right after the start variable that you declared earlier:

```js
// create a function to make a directions request
function getRoute(end) {
  // make a directions request using cycling profile
  // an arbitrary start will always be the same
  // only the end or destination will change
  var start = [-122.662323, 45.523751];
  var url = 'https://api.mapbox.com/directions/v5/mapbox/cycling/' + start[0] + ',' + start[1] + ';' + end[0] + ',' + end[1] + '?steps=true&geometries=geojson&access_token=' + mapboxgl.accessToken;

  // make an XHR request https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest
  var req = new XMLHttpRequest();
  req.responseType = 'json';
  req.open('GET', url, true);
  req.onload = function() {
    var data = req.response.routes[0];
    var route = data.geometry.coordinates;
    var geojson = {
      type: 'Feature',
      properties: {},
      geometry: {
        type: 'LineString',
        coordinates: route
      }
    };
    // if the route already exists on the map, reset it using setData
    if (map.getSource('route')) {
      map.getSource('route').setData(geojson);
    } else { // otherwise, make a new request
      map.addLayer({
        id: 'route',
        type: 'line',
        source: {
          type: 'geojson',
          data: {
            type: 'Feature',
            properties: {},
            geometry: {
              type: 'LineString',
              coordinates: geojson
            }
          }
        },
        layout: {
          'line-join': 'round',
          'line-cap': 'round'
        },
        paint: {
          'line-color': '#3887be',
          'line-width': 5,
          'line-opacity': 0.75
        }
      });
    }
    // add turn instructions here at the end
  };
  req.send();
}

map.on('load', function() {
  // make an initial directions request that
  // starts and ends at the same location
  getRoute(start);

  // Add starting point to the map
  map.addLayer({
    id: 'point',
    type: 'circle',
    source: {
      type: 'geojson',
      data: {
        type: 'FeatureCollection',
        features: [{
          type: 'Feature',
          properties: {},
          geometry: {
            type: 'Point',
            coordinates: start
          }
        }
        ]
      }
    },
    paint: {
      'circle-radius': 10,
      'circle-color': '#3887be'
    }
  });
  // this is where the code from the next step will go
});
```

{{
  <Note title='Mapbox JavaScript SDK' imageComponent={<BookImage />}>
    <p>Mapbox also offers a JavaScript SDK, a node.js and browser JavaScript client, to interact with our web services directly in your web applications. You can use the JavaScript SDK to make the Directions API request directly. For more information on the Mapbox JavaScript SDK see the <a href="https://github.com/mapbox/mapbox-sdk-js/blob/master/docs/services.md">documentation on GitHub</a>.</p>
  </Note>
}}

Now that you've constructed the function that makes the requests and draws the routes, you'll want to load in an initial route from our starting point.

To see if this is working, open your browser's console (`Command+Alt+J` on a Mac, `Ctrl+Alt+J` on Windows) where you can interact with the application you've written so far. In the console, type `getRoute([-122.677738,45.522458])` to execute your function and pass in coordinates for a location in downtown Porland, OR. If everything is working, you should see a line drawn from the east side of the river to the west.

{{
  <DemoIframe src="/help/demos/directions-api/demo-one.html" />
}}

## Add your origin and destination

Now that you've created the start point (`getRoute(start)`) you'll provide a way to let the user select a destination. Add the next bit of code that allows the user to click the map and update the location of the destination:

```js
map.on('click', function(e) {
  var coordsObj = e.lngLat;
  canvas.style.cursor = '';
  var coords = Object.keys(coordsObj).map(function(key) {
    return coordsObj[key];
  });
  var end = {
    type: 'FeatureCollection',
    features: [{
      type: 'Feature',
      properties: {},
      geometry: {
        type: 'Point',
        coordinates: coords
      }
    }
    ]
  };
  if (map.getLayer('end')) {
    map.getSource('end').setData(end);
  } else {
    map.addLayer({
      id: 'end',
      type: 'circle',
      source: {
        type: 'geojson',
        data: {
          type: 'FeatureCollection',
          features: [{
            type: 'Feature',
            properties: {},
            geometry: {
              type: 'Point',
              coordinates: coords
            }
          }]
        }
      },
      paint: {
        'circle-radius': 10,
        'circle-color': '#f30'
      }
    });
  }
  getRoute(coords);
});
```

{{
  <DemoIframe src="/help/demos/directions-api/demo-two.html" />
}}

## Add turn instructions

Because you added the `steps=true` parameter to the initial request, all the instructions for navigating the route are available to parse. Now add these steps to the sidebar in the div element called `instructions`.

```js
// get the sidebar and add the instructions
var instructions = document.getElementById('instructions');
var steps = data.legs[0].steps;

var tripInstructions = [];
for (var i = 0; i < steps.length; i++) {
  tripInstructions.push('<br><li>' + steps[i].maneuver.instruction) + '</li>';
  instructions.innerHTML = '<br><span class="duration">Trip duration: ' + Math.floor(data.duration / 60) + ' min 🚴 </span>' + tripInstructions;
}
```

In the directions response object, turn instructions are stored in the `routes` property. You can find `instructions` inside `routes` > `legs` > `steps` > `maneuver`. Each `instruction` is a string that describes what the bicycle rider should do next along a route.

Next, add some CSS to style the `div` so it appears on the left side of your map and has a white background.

```css
#instructions {
  position: absolute;
  margin: 20px;
  width: 25%;
  top: 0;
  bottom: 20%;
  padding: 20px;
  background-color: rgba(255, 255, 255, 0.9);
  overflow-y: scroll;
  font-family: sans-serif;
  font-size: 0.8em;
  line-height: 2em;
}

.duration {
  font-size: 2em;
}
```

## Finished product

You've used the Mapbox Directions API and Mapbox GL JS to add a bicycle route to a map.

{{
  <DemoIframe src="/help/demos/directions-api/index.html" />
}}

## Next steps

Now that you have practiced using the Mapbox Directions API, read about additional options in the [Directions API documentation](https://docs.mapbox.com/api/navigation/#directions). You can also try adding more details to your application:

- Style the origin and destination uniquely.
- Use the [Mapbox Geocoding API](https://docs.mapbox.com/api/search/#geocoding) to assign the start and end points based on user input.
- Add more details, like distance and duration, to the turn instructions.
- Explore other ways to integrate directions services, including turn-by-turn instructions, into your applications including the [Mapbox GL directions plugin](https://github.com/mapbox/mapbox-gl-directions), the [JavaScript SDK](https://github.com/mapbox/mapbox-sdk-js#mapbox-sdk-js), and the Mapbox Navigation SDKs for [iOS](https://docs.mapbox.com/ios/navigation/overview/) and [Android](https://docs.mapbox.com/android/navigation/overview/).

Don't forget to explore other directions-related services like the [Mapbox Matrix API](https://docs.mapbox.com/api/navigation/#matrix) and [Optimization API](https://docs.mapbox.com/api/navigation/#optimization).
