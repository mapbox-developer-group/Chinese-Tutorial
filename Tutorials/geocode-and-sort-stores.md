---
title: Sort stores by distance
description: This guide walks you through all the code that you need to build a store locator which lets you search for the nearest location.
thumbnail: geocodeAndSort
level: 3
language:
- JavaScript
prereq: Familiarity with front-end development concepts. Some advanced JavaScript required.
topics:
- web apps
- geocoding
prependJs:
  - "import Icon from '@mapbox/mr-ui/icon';"
  - "import DemoIframe from '@mapbox/dr-ui/demo-iframe';"
  - "import * as constants from '../../constants';"
  - "import Note from '@mapbox/dr-ui/note';"
  - "import BookImage from '@mapbox/dr-ui/book-image';"
contentType: tutorial
---

This guide will walk you through how to use [Mapbox GL JS](https://www.mapbox.com/mapbox-gl-js/), the [Mapbox GL Geocoder plugin](https://github.com/mapbox/mapbox-gl-geocoder), and [Turf.js](http://turfjs.org/) to sort store locations based on distance from a geocoded point. This guide extends the map created in the [Build a store locator using Mapbox GL JS](/help/tutorials/building-a-store-locator) tutorial. If haven't completed that tutorial yet, be sure to do so before starting this project. If you're new to Mapbox GL JS, you may also want to read our [Web applications guide](/help/how-mapbox-works/web-apps) first.

{{
  <DemoIframe src="/help/demos/geocode-and-sort/index.html" />
}}

## Getting started

For this project, we recommend that you create a local folder called "sort-store-locator" to house your project files. You'll see this folder referred to as your *project folder*.

There are a few resources you'll need before getting started:

- __Store locator final project__. This tutorial builds off of the code created in the [Build a store locator using Mapbox GL JS](/help/tutorials/building-a-store-locator) tutorial. Make sure you've created a copy of the final version of that code for this new project or downloaded the starter code. <a href="/help/demos/geocode-and-sort/starter-code.zip">{{<Icon name='arrow-down' inline={true} />}} Download starter code</a>
- [__An access token__](/help/glossary/access-token/) from your account. You will use an access token to associate a map with your account. Your access token is on the  [Account page](https://account.mapbox.com/).
- [__Mapbox GL JS__](https://www.mapbox.com/mapbox-gl-js/). The Mapbox JavaScript library that uses WebGL to render interactive maps from Mapbox GL styles.
- [__Mapbox GL Geocoder__](https://www.mapbox.com/mapbox-gl-js/plugins/) plug-in. The Mapbox GL JS wrapper library for the [Mapbox Geocoding API](https://docs.mapbox.com/api/search/#geocoding).
- [__Turf.js__](http://turfjs.org). An open-source analysis library that performs spatial analysis in the browser and in Node.js.
- __A text editor.__ You'll be writing HTML, CSS, and JavaScript.

## Add plugins and initialize the map

Download the `starter-code` zip file. Inside you'll find an `index.html` file and an `img` folder that contains the custom marker you'll be using to show store locations. Open the `index.html` file in a text editor. Make sure you use your own access token and set it equal to `mapboxgl.accessToken`.

### Add Mapbox GL geocoder plugin and Turf.js

Next, set up your document by adding the Mapbox GL Geocoder plug-in and Turf.js library links to the `head` of your HTML file. Copy and paste the following code after your links to Mapbox GL JS.

```html
  <!-- Geocoder plugin -->
  <script src='https://api.mapbox.com/mapbox-gl-js/plugins/mapbox-gl-geocoder/{{constants.VERSION_GLJS_GEOCODER_PLUGIN}}/mapbox-gl-geocoder.min.js'></script>
  <link rel='stylesheet' href='https://api.mapbox.com/mapbox-gl-js/plugins/mapbox-gl-geocoder/{{constants.VERSION_GLJS_GEOCODER_PLUGIN}}/mapbox-gl-geocoder.css' type='text/css' />

  <!-- Turf.js plugin -->
  <script src='https://npmcdn.com/@turf/turf/turf.min.js'></script>
```

### Add geocoder control

Add the geocoder control to your JavaScript code using the constructor `new mapboxgl.Geocoder`. In this case, you'll limit the search results to the Washington DC area using the `bbox` parameter. There are several other parameters you can specify. You can read more about the available parameters in the [documentation on GitHub](https://github.com/mapbox/mapbox-gl-geocoder/blob/master/API.md).

The code below should be added inside `map.on('load', function (e) { ... });` in your `script` tags.

```js
var geocoder = new MapboxGeocoder({
  accessToken: mapboxgl.accessToken, // Set the access token
  mapboxgl: mapboxgl, // Set the mapbox-gl instance
  marker: false, // Do not use the default marker style
  bbox: [-77.210763, 38.803367, -76.853675, 39.052643] // Set the bounding box coordinates
});

map.addControl(geocoder, 'top-left');
```

Now add some CSS to style your new geocoding search bar. You can add this code right before your closing `</style>` tag.

```css
.mapboxgl-ctrl-geocoder {
  border: 0;
  border-radius: 0;
  position: relative;
  top: 0;
  width: 800px;
  margin-top: 0;
}

.mapboxgl-ctrl-geocoder > div {
  min-width: 100%;
  margin-left: 0;
}
```

Save your HTML document, and refresh the page in your web browser. The result should look like this.

{{
  <DemoIframe src="/help/demos/geocode-and-sort/step-one.html" />
}}

Notice what happens when you search for an address using the geocoding form you have created. The map will fly to the location you've specified, but doesn't visualize the matching location. In the next step, you'll add a point once you've successfully found a location using Mapbox GL Geocoder.

## Add point on search

{{<Note title="Adding a custom marker style" imageComponent={<BookImage />}>}}
  The Mapbox GL Geocoder sets a marker at the search result location by default. This example adds a custom marker as a new layer instead. If you want to use the default marker provided by the geocoder, remove the line `marker: false,` from the new geocoder instantiation.
{{</Note>}}

Now that your geocoder is working, you can write code to add a point to your map at the location you searched. All this code will go inside `map.on('load', function (e) { ... });` directly following the code you added in the previous step. First, you need to add an empty source using `map.addSource()` where you will store your geocoder result, and a styled layer from that source using `map.addLayer()`.

```js
map.addSource('single-point', {
  type: 'geojson',
  data: {
    type: 'FeatureCollection',
    features: [] // Notice that initially there are no features
  }
});

map.addLayer({
  id: 'point',
  source: 'single-point',
  type: 'circle',
  paint: {
    'circle-radius': 10,
    'circle-color': '#007cbf',
    'circle-stroke-width': 3,
    'circle-stroke-color': '#fff'
  }
});
```

Next, create an event listener that fires when the user selects a geocoder result. When the user selects a place from the list of returned locations, save the coordinates in a variable called `searchResult`. Then, set the data in the source with the id `single-point` you declared above to `searchResult`. Copy and paste this code after the `map.addSource()` and `map.addLayer()` functions.

```js
geocoder.on('result', function(ev) {
  var searchResult = ev.result.geometry;
  map.getSource('single-point').setData(searchResult);
});
```

The result should look like this:

{{
  <DemoIframe src="/help/demos/geocode-and-sort/step-two.html" />
}}

## Sort store list by distance

Next, calculate the distance between the searched location and the stores, add the results to your GeoJSON data, and sort the store listings by distance from the searched point.

### Find distance from all locations

Next you'll use Turf.js to find the distances between your new point and each of the restaurant locations. Turf.js can do a wide variety of spatial analysis functions, which you can read about in the [documentation](http://turfjs.org/docs/). In this tutorial you are going to use [**distance**](http://turfjs.org/docs/#distance).

Within your `geocoder.on('result', function(){...});` function, use a `forEach` loop to iterate through all the store locations in your GeoJSON (remember, you stored these in the `stores` variable earlier), define a new property for each object called `distance`, and set the value of that property to the distance between the coordinates stored in the `searchResult` and the coordinates of each store location. You will do this using the `turf.distance()` method, which accepts three arguments: `from, to, options`.

```js
var options = { units: 'miles' };
stores.features.forEach(function(store) {
  Object.defineProperty(store.properties, 'distance', {
    value: turf.distance(searchResult, store.geometry, options),
    writable: true,
    enumerable: true,
    configurable: true
  });
});
```

For each feature in your GeoJSON, a `distance` property is applied or will be updated each time a new geocoder result is selected.

#### Sort store list by distance

Now that you have the `distance` value for each store location, you can use it to sort the list of stores by distance.

First, sort the objects in the `stores` array by the `distance` property you added earlier. Copy and paste the following code snippet inside the `geocoder.on('result', function(){...});` function.

```js
stores.features.sort(function(a, b) {
  if (a.properties.distance > b.properties.distance) {
    return 1;
  }
  if (a.properties.distance < b.properties.distance) {
    return -1;
  }
  // a must be equal to b
  return 0;
});
```

Then, remove the current list of stores and rebuild the list using the reordered array you created. The individual listings are nested within the `div` with id `listings`.

```js
var listings = document.getElementById('listings');
while (listings.firstChild) {
  listings.removeChild(listings.firstChild);
}

buildLocationList(stores);
```

Now the listing for each store will be in ascending order of distance from the point that was searched. To make the new list of locations more useful to your viewers, add text that describes each listing's distance from the point they searched for. When you built your initial interactive store locator in the previous tutorial, you created a `buildLocationListing()` function. You will need to find and change that function to check if there is a `distance` property, and if there is, add the value of that property to each listing. Copy and paste the following code before the `link.addEventListener()` function within the `buildLocationListing()` function.

```js
if (prop.distance) {
  var roundedDistance = Math.round(prop.distance * 100) / 100;
  details.innerHTML += '<p><strong>' + roundedDistance + ' miles away</strong></p>';
}
```

The result should look like this:

{{
  <DemoIframe src="/help/demos/geocode-and-sort/step-three.html" />
}}

## Fit bounds to search result and closest store

Finally, when you search for a location, you can change the view to include both the location that was searched and the closest store to show more context. You can do this by using `map.fitBounds()` and specifying a [bounding box](/help/glossary/bounding-box/). But the bounds need to be in a specific order. The first point you specify should be the lower left corner of the bounding box, and the second should be the upper right corner. Add the following code inside the `geocoder.on()` function to create a `bbox` with this syntax from the geocoded location and the closest store, fly to it, and open the closest store's popup.

```js
function sortLonLat(storeIdentifier) {
  var lats = [stores.features[storeIdentifier].geometry.coordinates[1], searchResult.coordinates[1]];
  var lons = [stores.features[storeIdentifier].geometry.coordinates[0], searchResult.coordinates[0]];

  var sortedLons = lons.sort(function(a, b) {
    if (a > b) {
      return 1;
    }
    if (a.distance < b.distance) {
      return -1;
    }
    return 0;
  });
  var sortedLats = lats.sort(function(a, b) {
    if (a > b) {
      return 1;
    }
    if (a.distance < b.distance) {
      return -1;
    }
    return 0;
  });

  map.fitBounds([
    [sortedLons[0], sortedLats[0]],
    [sortedLons[1], sortedLats[1]]
  ], {
    padding: 100
  });
}

sortLonLat(0);
createPopUp(stores.features[0]);
```

## Finished product

You have created a store locator with geocoding and spatial analysis.

{{
  <DemoIframe src="/help/demos/geocode-and-sort/index.html" />
}}

## Next steps

After this guide, you should have everything you need to create your own store locator. You can complete the [Create a custom style tutorial](/help/tutorials/create-a-custom-style/) to create a branded map style or use [Cartogram](https://apps.mapbox.com/cartogram/), a drag and drop tool, to create a custom style from your logo in minutes. To do more with Mapbox GL JS, explore our [examples page](https://www.mapbox.com/mapbox-gl-js/examples/) and the Mapbox GL JS on the [help page](/help/tutorials/).
