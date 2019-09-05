---
title: Generate an optimized route
description: Use the Mapbox Optimization API to generate a duration-optimized route between several points.
thumbnail: optimizationApi
level: 3
platform: web
topics:
- web apps
- directions
language:
- JavaScript
prereq: Advanced JavaScript required.
prependJs:
  - "import * as constants from '../../constants';"
  - "import Note from '@mapbox/dr-ui/note';"
  - "import BookImage from '@mapbox/dr-ui/book-image';"
  - "import Icon from '@mapbox/mr-ui/icon';"
  - "import UserAccessToken from '../../components/user-access-token';"
  - "import DemoIframe from '@mapbox/dr-ui/demo-iframe';"
contentType: tutorial
---

The Mapbox Optimization API returns a duration-optimized route between up to 12 coordinates. In this guide, you will build an application that allows you to click multiple points on a map and create an optimized delivery route using the Optimization API.

{{
  <DemoIframe src="/help/demos/optimization-api/step-five.html" />
}}

Throughout the guide you'll create a custom marker to represent a delivery vehicle, add a warehouse location to the map, add a marker icon when a user clicks on the map, and build an optimized route between those points in real time.

## Getting started

Here are the resources that you'll use throughout this guide:

- **Mapbox account and access token.** Sign up for an account at [mapbox.com/signup](https://www.mapbox.com/signup/). You can find your [access tokens](/help/how-mapbox-works/access-tokens/) on your [Account page](https://account.mapbox.com/).
- **Mapbox GL JS.** [Mapbox GL JS](https://www.mapbox.com/mapbox-gl-js/) is our JavaScript library that uses WebGL to render interactive web maps from Mapbox GL styles.
- **Turf.js.** [Turf](http://turfjs.org/) is a JavaScript library that allows you to add geospatial analysis to your map.
- **Mapbox Optimization API.** Our [Optimization API](https://docs.mapbox.com/api/navigation/#optimization) will help you generate optimal delivery routes for multiple stops across an entire fleet.
- **jQuery.** [jQuery](https://jquery.com/) is a JavaScript library you will use to add your API request to your application.

## Initialize the map

Start by initializing a map with Mapbox GL JS. Create a new HTML file and use the code below to initialize a map centered on Detroit, Michigan. This code also references a couple scripts in the `head` and declares a few JavaScript variables that you will need in later steps.

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset='utf-8' />
    <title>Delivery App</title>
    <meta name='viewport' content='initial-scale=1,maximum-scale=1,user-scalable=no' />
    <script src='https://npmcdn.com/@turf/turf/turf.min.js'></script>
    <script src='https://ajax.googleapis.com/ajax/libs/jquery/3.1.1/jquery.min.js'></script>
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
        right: 0;
        left: 0;
      }
    </style>
  </head>
  <body>
    <div id='map' class='contain'></div>
    <script>
      var truckLocation = [-83.093, 42.376];
      var warehouseLocation = [-83.083, 42.363];
      var lastQueryTime = 0;
      var lastAtRestaurant = 0;
      var keepTrack = [];
      var currentSchedule = [];
      var currentRoute = null;
      var pointHopper = {};
      var pause = true;
      var speedFactor = 50;

      // Add your access token
      mapboxgl.accessToken = '{{ <UserAccessToken /> }}';

      // Initialize a map
      var map = new mapboxgl.Map({
        container: 'map', // container id
        style: 'mapbox://styles/mapbox/light-v{{constants.VERSION_LIGHT_STYLE}}', // stylesheet location
        center: truckLocation, // starting position
        zoom: 12 // starting zoom
      });
    </script>
  </body>
</html>
```

Open the file in your browser, and you will see a map centered on Detroit.

{{
  <DemoIframe src="/help/demos/optimization-api/step-one.html" />
}}

## Set up the map

Next, add the location of a delivery truck and the pick up location.

### Add truck location

There are several ways to add point data using Mapbox GL JS. In this guide you'll create an HTML DOM element for each marker and bind it to a coordinate using the Mapbox GL JS [`Marker`](https://www.mapbox.com/mapbox-gl-js/api/#marker) method. When you add a marker using the Marker method, you are attaching an empty `div` to the point. You'll need to specify the style of the marker before adding it to the map.

Start by adding the `truck` class between the `style` tags.

```css
.truck {
  margin: -10px -10px;
  width: 20px;
  height: 20px;
  border: 2px solid #fff;
  border-radius: 50%;
  background: #3887be;
  pointer-events: none;
}
```

Next, add a marker to the map using `mapboxgl.Marker`. To make sure the rest of the code can execute, it needs to live in a *callback function* that is executed when the map is finished loading.

{{
  <Note
    imageComponent={<BookImage />}
    title='What is a callback?'
  >
    <p>Initializing the map on the page does more than create a container in the <code>map</code> div: it also tells the browser to request the Mapbox Studio style you created in part 1. This can take variable amounts of time depending on how quickly the Mapbox server can respond to that request, and everything else you're going to add in the code relies on that style being loaded onto the map. As such, it's important to make sure the style is loaded before any more code is executed.</p><p>Fortunately, the map object can tell your browser about certain events that occur when the map's state changes. One of these events is <code>load</code>, which is emitted when the style has been loaded onto the map. When you use the <code>map.on</code> method, you can make sure that the rest of your code is executed *only* after the map has finished loading by placing it in a <a href='https://github.com/maxogden/art-of-node#callbacks'>callback function</a> that is called when the <code>load</code> event occurs.</p>
  </Note>
}}

In the previous step, you declared a variable called `truckLocation` that contains an array of two numbers (longitude and latitude). Use `truckLocation` as the coordinate for the truck marker using `setLngLat`.

{{
  <Note
    imageComponent={<BookImage />}
  >
    <p>In this guide you are using a static point as the location of the delivery truck. In your application, you could set the longitude and latitude using the location of physical devices such as the location of a phone or tablet, collecting pings from IoT devices, or GPS signals from vehicle locations.</p>
  </Note>
}}

Use the code below to add a marker once the map has loaded.

```js
map.on('load', function() {
  var marker = document.createElement('div');
  marker.classList = 'truck';

  // Create a new marker
  truckMarker = new mapboxgl.Marker(marker)
    .setLngLat(truckLocation)
    .addTo(map);
});
```


### Add warehouse location

Now add the warehouse location to the map. This will be where the delivery truck has to go to pick up items to deliver. Start by creating a GeoJSON feature collection that includes a single point feature that describes where the warehouse is located. The [Turf.js](http://turfjs.org) `featureCollection` method is a convenient way to turn a coordinate, or series of coordinates, into a GeoJSON feature collection. Add the code below before your `map.on('load', function(){});` callback. Note that the `warehouseLocation` variable is a latitude, longitude pair that was declared in the first code block you copied when initializing your map.

```js
// Create a GeoJSON feature collection for the warehouse
var warehouse = turf.featureCollection([turf.point(warehouseLocation)]);
```

Then, within the `map.on('load', function())` callback, create two new layers &mdash; a circle layer and a symbol layer. Both layers will use the `warehouse` GeoJSON feature collection as the data source.

```js
// Create a circle layer
map.addLayer({
  id: 'warehouse',
  type: 'circle',
  source: {
    data: warehouse,
    type: 'geojson'
  },
  paint: {
    'circle-radius': 20,
    'circle-color': 'white',
    'circle-stroke-color': '#3887be',
    'circle-stroke-width': 3
  }
});

// Create a symbol layer on top of circle layer
map.addLayer({
  id: 'warehouse-symbol',
  type: 'symbol',
  source: {
    data: warehouse,
    type: 'geojson'
  },
  layout: {
    'icon-image': 'grocery-15',
    'icon-size': 1
  },
  paint: {
    'text-color': '#3887be'
  }
});
```

Refresh your application and you'll see a map displaying the location of the delivery truck and the warehouse.

{{
  <DemoIframe src="/help/demos/optimization-api/step-two.html" />
}}

## Add drop-off locations on click

In an application that generates optimized routes between several points, there are many different ways you could generate the points: a user could input addresses, a user could select coordinates on the map, or you could pull data in from an external source. In this guide, you'll allow the user to select points by clicking on the map.

A request to the Optimization API must contain 2-12 coordinates. In this guide:

- You'll use the default `roundtrip=true`. This means that the first coordinate is both the start and end point of the trip. (This is helpful if the delivery truck needs to return to a depot.) Both the start and the end point will be counted toward the 12 coordinate limit.
- The pick up location will also be counted toward the 12 coordinate limit.
- As a result, the user can select up to 9 points &mdash; the 12 coordinate limit less the truck location as both the start and finish (2 coordinates) and the pick up location (1 coordinate).

### Add a new layer

Start by creating a new layer that contains all the drop-off locations.

Create an empty GeoJSON feature collection. Later you'll store drop-off locations in this feature collection when the map is clicked. Add this directly after the `warehouse` variable you added above.

```js
// Create an empty GeoJSON feature collection for drop-off locations
var dropoffs = turf.featureCollection([]);
```

Then, within `map.on('load', function())`, add a new layer called `dropoffs-symbol`, which will display all the drop-off locations. Layers in Mapbox GL JS require a `source`, but the user hasn't selected any drop-off locations yet, so you will need to provide an empty GeoJSON feature collection as a starting point. When the map is first initialized, the data source will be the empty `dropoffs` feature collection you defined above. Later, after the user clicks on the map, the points that are clicked will be added to the `dropoffs` feature collection and the data source for the layer will update.

```js
map.addLayer({
  id: 'dropoffs-symbol',
  type: 'symbol',
  source: {
    data: dropoffs,
    type: 'geojson'
  },
  layout: {
    'icon-allow-overlap': true,
    'icon-ignore-placement': true,
    'icon-image': 'marker-15',
  }
});
```

### Add click listener

You'll need to listen for when a user clicks on the map. Add a click listener inside the `map.on('load', function())` callback. Inside the click listener, add a two new functions `newDropoff` and `updateDropoffs`, which will be called every time the map is clicked.

```js
// Listen for a click on the map
map.on('click', function(e) {
  // When the map is clicked, add a new drop-off point
  // and update the `dropoffs-symbol` layer
  newDropoff(map.unproject(e.point));
  updateDropoffs(dropoffs);
});
```

Build out the `newDropoff` and `updateDropoffs` functions. When a user clicks on the map, you will make a new request for delivery. Two things will happen when a user makes a new request: you'll create a new drop-off up location and you'll update the data source for the `dropoffs-symbol` layer.

Add the following code outside of your `map.on('load', function())` callback.

```js
function newDropoff(coords) {
  // Store the clicked point as a new GeoJSON feature with
  // two properties: `orderTime` and `key`
  var pt = turf.point(
    [coords.lng, coords.lat],
    {
      orderTime: Date.now(),
      key: Math.random()
    }
  );
  dropoffs.features.push(pt);
}

function updateDropoffs(geojson) {
  map.getSource('dropoffs-symbol')
    .setData(geojson);
}
```

Refresh your application. When you click on the map, a new marker symbol that is a drop-off location will be added to the map.

{{
  <DemoIframe src="/help/demos/optimization-api/step-three.html" />
}}

## Generate and add a route

Next, you'll build a request for the Optimization API, add the route from the response to the map, and style the route.

### Create a layer with an empty source

Like in the previous step, create an empty GeoJSON feature collection, which will later contain the route after the map is clicked and a route is generated. Add this line of code immediately after you declare the `dropoffs` variable.

```js
// Create an empty GeoJSON feature collection, which will be used as the data source for the route before users add any new data
var nothing = turf.featureCollection([]);
```

Within `map.on('load', function())`, directly after the code you wrote to add the location of the warehouse as a layer, add a new layer with an empty source. You will use this to display the route after you make the API request.

```js
map.addSource('route', {
  type: 'geojson',
  data: nothing
});

map.addLayer({
  id: 'routeline-active',
  type: 'line',
  source: 'route',
  layout: {
    'line-join': 'round',
    'line-cap': 'round'
  },
  paint: {
    'line-color': '#3887be',
    'line-width': [
      "interpolate",
      ["linear"],
      ["zoom"],
      12, 3,
      22, 12
    ]
  }
}, 'waterway-label');
```

### Build the request

Next, build the request to the Optimization API to generate a route. Your request will include several parameters:

- `profile`: This is the mode of transportation. You'll be using the `driving` profile.
- `coordinates`: This is a semicolon-separated list of `{longitude},{latitude}` coordinates. There must be between 2 and 12 coordinates. In this guide, the list of coordinates includes the starting location of the truck, the warehouse, up to nine drop-off locations, and the location where the truck started.
- `distributions`: This is a semicolon-separated list of number pairs that correspond with the coordinates list. The first number indicates the index to the coordinate of the pick-up location in the coordinates list, and the second number indicates the index to the coordinate of the drop-off location in the coordinates list. Each pair must contain exactly two numbers. Pick-up and drop-off locations in one pair cannot be the same. The returned solution will visit pick-up locations before visiting drop-off locations.

Add the following after the `updateDropoffs` function you added in the previous section.

```js
// Here you'll specify all the parameters necessary for requesting a response from the Optimization API
function assembleQueryURL() {

  // Store the location of the truck in a variable called coordinates
  var coordinates = [truckLocation];
  var distributions = [];
  keepTrack = [truckLocation];

  // Create an array of GeoJSON feature collections for each point
  var restJobs = objectToArray(pointHopper);

  // If there are any orders from this restaurant
  if (restJobs.length > 0) {

    // Check to see if the request was made after visiting the restaurant
    var needToPickUp = restJobs.filter(function(d, i) {
      return d.properties.orderTime > lastAtRestaurant;
    }).length > 0;

    // If the request was made after picking up from the restaurant,
    // Add the restaurant as an additional stop
    if (needToPickUp) {
      var restaurantIndex = coordinates.length;
      // Add the restaurant as a coordinate
      coordinates.push(warehouseLocation);
      // push the restaurant itself into the array
      keepTrack.push(pointHopper.warehouse);
    }

    restJobs.forEach(function(d, i) {
      // Add dropoff to list
      keepTrack.push(d);
      coordinates.push(d.geometry.coordinates);
      // if order not yet picked up, add a reroute
      if (needToPickUp && d.properties.orderTime > lastAtRestaurant) {
        distributions.push(restaurantIndex + ',' + (coordinates.length - 1));
      }
    });
  }

  // Set the profile to `driving`
  // Coordinates will include the current location of the truck,
  return 'https://api.mapbox.com/optimized-trips/v1/mapbox/driving/' + coordinates.join(';') + '?distributions=' + distributions.join(';') + '&overview=full&steps=true&geometries=geojson&source=first&access_token=' + mapboxgl.accessToken;
}

function objectToArray(obj) {
  var keys = Object.keys(obj);
  var routeGeoJSON = keys.map(function(key) {
    return obj[key];
  });
  return routeGeoJSON;
}
```

### Make the request

Use [jQuery](https://api.jquery.com/jquery.ajax/) to make the request. There are several things going on in the code below:

- **Make the request**. Make a request to the Optimization API using the URL that you assembled in the `assembleQueryURL()` function in the previous step.
- **Create a GeoJSON feature collection**. The API response will include an array of `trips`. Use the first trip in this array (`trip[0]`) to create a GeoJSON feature collection that contains the route.
- **Update the route data**. Before the user interacts with the map, the `route` source is an empty GeoJSON feature collection. Update the `route` source from an empty feature collection to the `trip` returned in the API response. Then check if a trip exists:
  - If there is no trip available, use the empty `nothing` source.
  - If there is a trip, get the `route` source and set the data equal to `routeGeoJSON`.
- **Display a warning message when reaching coordinate limit**. The user can select up to nine points on the map. When the user reaches that limit, display a warning message that they cannot add any more points to the route.

All this will happen within the existing `newDropoff` function, meaning there will be a request to the Optimization API every time there is a new dropoff location specified &mdash; whenever a user clicks on the map.

Update the existing `newDropoff` function and add the API request using the code below.

```js
function newDropoff(coords) {
  // Store the clicked point as a new GeoJSON feature with
  // two properties: `orderTime` and `key`
  var pt = turf.point(
    [coords.lng, coords.lat],
    {
      orderTime: Date.now(),
      key: Math.random()
    }
  );
  dropoffs.features.push(pt);
  pointHopper[pt.properties.key] = pt;

  // Make a request to the Optimization API
  $.ajax({
    method: 'GET',
    url: assembleQueryURL(),
  }).done(function(data) {
    // Create a GeoJSON feature collection
    var routeGeoJSON = turf.featureCollection([turf.feature(data.trips[0].geometry)]);

    // If there is no route provided, reset
    if (!data.trips[0]) {
      routeGeoJSON = nothing;
    } else {
      // Update the `route` source by getting the route source
      // and setting the data equal to routeGeoJSON
      map.getSource('route')
        .setData(routeGeoJSON);
    }

    if (data.waypoints.length === 12) {
      window.alert('Maximum number of points reached. Read more at docs.mapbox.com/api/navigation/#optimization.');
    }
  });
}
```

Refresh your app, select points on the map, and you will see a route drawn between all points.

{{
  <DemoIframe src="/help/demos/optimization-api/step-four.html" />
}}

### Add directionality to route line

With the current style, it's a bit difficult to understand the directionality of the route line. Add another layer called `routearrows` to help the map viewer understand which way the truck will be traveling along the route. The `routearrows` layer will use the same data source as the `routeline-active` layer. Instead of a line layer, use a symbol layer with arrows indicating the directionality of routes along the line.

Add the following code inside the `map.on('load', function())` callback function.

```js
map.addLayer({
  id: 'routearrows',
  type: 'symbol',
  source: 'route',
  layout: {
    'symbol-placement': 'line',
    'text-field': '▶',
    'text-size': [
      "interpolate",
      ["linear"],
      ["zoom"],
      12, 24,
      22, 60
    ],
    'symbol-spacing': [
      "interpolate",
      ["linear"],
      ["zoom"],
      12, 30,
      22, 160
    ],
    'text-keep-upright': false
  },
  paint: {
    'text-color': '#3887be',
    'text-halo-color': 'hsl(55, 11%, 96%)',
    'text-halo-width': 3
  }
}, 'waterway-label');
```

Refresh your app, select points on the map, and you will see a route with arrows drawn between all points.

## Final product

You used the Optimization API to build a web application that allows a user to choose multiple points on a map, makes an API request, and displays an optimized route in real-time.

{{
  <DemoIframe src="/help/demos/optimization-api/step-five.html" />
}}

## Next steps

Read the [Mapbox Optimization API documentation](https://docs.mapbox.com/api/navigation/#optimization) for more information or learn how to build a driver app for iOS and Android with our step-by-step tutorials:

- [Build a navigation app for iOS](/help/tutorials/ios-navigation-sdk)
- [Build a navigation app for Android](/help/tutorials/android-navigation-sdk)
