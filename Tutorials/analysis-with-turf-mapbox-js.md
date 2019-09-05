---
title: Analyze data with Turf.js and Mapbox.js
description: Using Turf.js, you can add some spatial analysis to your map to solve problems. This guide walks through an example of Turf.js and Mapbox.js in a real-world context.
thumbnail: analysisWithTurfMapboxJs
level: 2
topics:
- web apps
- analysis
language:
- JavaScript
prereq: Familiarity with front-end development concepts.
legacy: true
prependJs:
  - "import * as constants from '../../constants';"
  - "import Note from '@mapbox/dr-ui/note';"
  - "import BookImage from '@mapbox/dr-ui/book-image';"
  - "import { LegacyNote } from '../../components/legacy-note';"
  - "import { hospitalsLex } from '../../snippets/hospitals-lex';"
  - "import { librariesLex } from '../../snippets/libraries-lex';"
  - "import UserAccessToken from '../../components/user-access-token';"
  - "import DemoIframe from '@mapbox/dr-ui/demo-iframe';"
contentType: tutorial
---

{{
  <LegacyNote
    legacyProduct='Mapbox.js'
    alternativeResource={{
      title: 'Analyze data with Turf.js and Mapbox GL JS',
      link: '/help/tutorials/analysis-with-turf/'
    }}
  />
}}

This guide walks you through how to use [Turf.js](http://turfjs.org), a JavaScript library for spatial analysis and statistics.

Let's say you are part of a team that manages health and safety for the libraries in Lexington, KY. One important part of your preparedness mandate is to know __which hospital is closest to each library__ in case there's an emergency at one of your facilities. This example will walk you through making a map of libraries and hospitals; when a user clicks on a library, the map will show which hospital is nearest.

{{
  <DemoIframe gl={false} src="/help/demos/turfjs-intro-js/demo-five.html" />
}}

## Getting started

There are a few resources you'll need to get started:

- [__A tileset ID__](/help/glossary/tileset-id). An ID points to a unique map you have created on Mapbox.
- [__An access token__](/help/glossary/access-token/). The token is used to associate a map with your account:

```js
L.mapbox.accessToken = '{{ <UserAccessToken /> }}';
```

- [__Mapbox.js__](https://www.mapbox.com/mapbox.js/). The Mapbox JavaScript API for building maps.
- [__Turf.js__](http://turfjs.org/). Turf is the JavaScript library you'll be using today to add analysis to your map.
- __Data.__ This example uses two data files: hospitals in Lexington, KY and libraries in Lexington, KY.
- __A text editor.__ You'll be writing HTML, CSS, and JavaScript.

## Add structure

For this guide, you will include the latest versions of Mapbox.js and Turf.js. Create a new HTML file in your text editor, and add these libraries to the head by copying the snippet below:

```html
<link href='https://api.mapbox.com/mapbox.js/{{constants.VERSION_MAPBOXJS}}/mapbox.css' rel='stylesheet' />
<script src='https://api.mapbox.com/mapbox.js/{{constants.VERSION_MAPBOXJS}}/mapbox.js'></script>
<script src='https://api.mapbox.com/mapbox.js/plugins/turf/{{constants.VERSION_TURF}}/turf.min.js'></script>
```

Now, add your map element. First, in the `body`, create an empty `div` for your map:

```html
<div id='map'></div>
```

Next, add some CSS to a `style` element in the `head` so your map takes up the width of the page:

```css
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
```

## Initialize a map

Now that your page has some nice structure to it, go ahead and get a map on the page using Mapbox.js.

You'll create a `L.mapbox.map` object called `map` and use `setView` to center the map on Lexington, KY. This is where you'll need to use your access token and tileset ID. Add the following script inside the `<body>` after the HTML:

```js
L.mapbox.accessToken = '{{ <UserAccessToken /> }}';
var map = L.mapbox.map('map')
  .setView([38.05, -84.5], 12)
  .addLayer(L.mapbox.styleLayer('mapbox://styles/mapbox/light-v10'));
map.scrollWheelZoom.disable();
```

{{
  <DemoIframe gl={false} src="/help/demos/turfjs-intro-js/demo-one.html" />
}}

Sweet! Now your page has a map centered on Lexington, KY.

{{
  <Note imageComponent={<BookImage />}>
    <p>There is an additional line in the code above that turns off scroll zoom on the map. This is optional.</p>
  </Note>
}}


## Load data

As mentioned above, this example uses two data files: libraries and hospitals in Lexington, KY, each of them is a GeoJSON FeatureCollection. In the next step, you'll add them to the map as `L.mapbox.featureLayer` objects and add a little code to make sure they're styled differently from each other. Also, you'll make sure that your map view contains all the points by fitting the map bounds to your features:

```js
L.mapbox.accessToken = '{{ <UserAccessToken /> }}';

// store GeoJSON objects in these variables
var hospitals = {{ hospitalsLex }};
var libraries = {{ librariesLex }};

// Add marker color, symbol, and size to hospital GeoJSON
for (var i = 0; i < hospitals.features.length; i++) {
  hospitals.features[i].properties['marker-color'] = '#DC143C';
  hospitals.features[i].properties['marker-symbol'] = 'hospital';
  hospitals.features[i].properties['marker-size'] = 'small';
}

// Add marker color, symbol, and size to library GeoJSON
for (var j = 0; j < libraries.features.length; j++) {
  libraries.features[j].properties['marker-color'] = '#4169E1';
  libraries.features[j].properties['marker-symbol'] = 'library';
  libraries.features[j].properties['marker-size'] = 'small';
}

var map = L.mapbox.map('map')
  .setView([38.05, -84.5], 12)
  .addLayer(L.mapbox.styleLayer('mapbox://styles/mapbox/light-v10'));
map.scrollWheelZoom.disable();

var hospitalLayer = L.mapbox.featureLayer(hospitals)
  .addTo(map);
var libraryLayer = L.mapbox.featureLayer(libraries)
  .addTo(map);

// When map loads, zoom to libraryLayer features
map.fitBounds(libraryLayer.getBounds());
```

Note that `hospitalLayer` and `libraryLayer` are defined _after_ you create your `map` object; you must define them in this order to make sure they can be added to the map.

{{
  <DemoIframe gl={false} src="/help/demos/turfjs-intro-js/demo-two.html" />
}}

Alternatively, you can save the GeoJSON as one or two `.geojson` files and [load the files on to the map](https://www.mapbox.com/mapbox.js/example/v1.0.0/geojson-marker-from-url/). If you do this, you will need to run this application from a local web server otherwise, you will receive a [Cross-origin Resource Sharing](http://en.wikipedia.org/wiki/Cross-origin_resource_sharing) (CORS) error.

## Add interactivity

Your map users will want to know the names of the libraries and hospitals displayed on the map, so next you'll add some popups. For this map, add some popups to these features that appear when the user hovers over the markers. Insert this into your script after you've created `hospitalLayer` and `libraryLayer`:

```js
// Bind a popup to each feature in hospitalLayer and libraryLayer
hospitalLayer.eachLayer(function(layer) {
  layer.bindPopup('<strong>' + layer.feature.properties.Name + '</strong>', { closeButton: false });
}).addTo(map);
libraryLayer.eachLayer(function(layer) {
  layer.bindPopup(layer.feature.properties.Name, { closeButton: false });
}).addTo(map);

// Open popups on hover
libraryLayer.on('mouseover', function(e) {
  e.layer.openPopup();
});
hospitalLayer.on('mouseover', function(e) {
  e.layer.openPopup();
});
```

{{
  <DemoIframe gl={false} src="/help/demos/turfjs-intro-js/demo-three.html" />
}}

Next, you'll make your map of the libraries and hospitals in Lexington even more useful by adding some analysis.

## Use Turf

[Turf](http://turfjs.org) is a JavaScript library for adding spatial and statistical analysis to your web maps. It contains many commonly-used GIS tools (like buffer, union, and merge) as well as statistical analysis functions (like sum, median, and average).

Fortunately, Turf has some functions that will help you out here! You're going to update your map so that clicking on a library will show users which hospital is closest to that library.

As a first step, make an "event handler" for when someone clicks on a library marker. When an event occurs, like a click on a marker, the event handler tells the map what to do in response. Before, you created event handlers for hovering over hospital and library markers; now you're going to make one for clicks.

```js
libraryLayer.on('click', function(e) {});
```

This is the structure of an event handler; anything you want to happen on click goes inside of the braces `{}`. In this case, you want to use Turf to identify the nearest hospital to the clicked library and make that marker larger to identify it.

```js
libraryLayer.on('click', function(e) {
  // Get the GeoJSON from libraryFeatures and hospitalFeatures
  var libraryFeatures = libraryLayer.getGeoJSON();
  var hospitalFeatures = hospitalLayer.getGeoJSON();

  // Using Turf, find the nearest hospital to library clicked
  var nearestHospital = turf.nearest(e.layer.feature, hospitalFeatures);

  // Change the nearest hospital to a large marker
  nearestHospital.properties['marker-size'] = 'large';

  // Add the new GeoJSON to hospitalLayer
  hospitalLayer.setGeoJSON(hospitalFeatures);
});
```

{{
  <DemoIframe gl={false} src="/help/demos/turfjs-intro-js/demo-four.html" />
}}

Excellent! This is almost ready to go.

## Add finishing touches

<!--copyeditor ignore previously-->
When a user clicks on a library, the nearest hospital gets larger. But when the user click on a different library, or on the map, the previously-nearest hospital doesn't go back to a small marker again. To address this, add some code to make the popup for the nearest hospital open up when it gets larger.

Add the following function before the click event handler.

```js
// reset marker size to small
function reset() {
  var hospitalFeatures = hospitalLayer.getGeoJSON();
  for (var i = 0; i < hospitalFeatures.features.length; i++) {
    hospitalFeatures.features[i].properties['marker-size'] = 'small';
  }
  hospitalLayer.setGeoJSON(hospitalFeatures);
}
```

Then, inside of the click handler, add a function call to `reset()` and some code for making sure the nearest hospital opens a popup when it gets larger.

```js
libraryLayer.on('click', function(e) {
  // Reset any and all marker sizes to small
  reset();

  // Get the GeoJSON from libraryFeatures and hospitalFeatures
  var libraryFeatures = libraryLayer.getGeoJSON();
  var hospitalFeatures = hospitalLayer.getGeoJSON();

  // Using Turf, find the nearest hospital to library clicked
  var nearestHospital = turf.nearest(e.layer.feature, hospitalFeatures);

  // Change the nearest hospital to a large marker
  nearestHospital.properties['marker-size'] = 'large';

  // Add the new GeoJSON to hospitalLayer
  hospitalLayer.setGeoJSON(hospitalFeatures);

  // Bind popups to new hospitalLayer and open popup
  // for nearest hospital
  hospitalLayer.eachLayer(function(layer) {
    layer.bindPopup('<strong>' + layer.feature.properties.Name + '</strong>', { closeButton: false });
    if (layer.feature.properties['marker-size'] === 'large') {
      layer.openPopup();
    }
  });
});
```

Lastly, add a little bit of code at the end to reset all the markers to small when anywhere on the map is clicked (besides on a library).

```js
map.on('click', function(e) {
  reset();
});
```

{{
  <DemoIframe gl={false} src="/help/demos/turfjs-intro-js/demo-five.html" />
}}

## Finished product

Nicely done! You have successfully created a map that calculates which hospital is closest to each library dynamically. Your finished HTML file should look like this:

```html
<html>
<head>
<meta charset=utf-8 />
<title>Turf.js Map</title>
<meta name='viewport' content='initial-scale=1,maximum-scale=1,user-scalable=no' />
<script src='https://api.mapbox.com/mapbox.js/{{constants.VERSION_MAPBOXJS}}/mapbox.js'></script>
<link href='https://api.mapbox.com/mapbox.js/{{constants.VERSION_MAPBOXJS}}/mapbox.css' rel='stylesheet' />
<script src='https://api.mapbox.com/mapbox.js/plugins/turf/{{constants.VERSION_TURF}}/turf.min.js'></script>
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
    L.mapbox.accessToken = '{{ <UserAccessToken /> }}';

    var hospitals = {{ hospitalsLex }};
    var libraries = {{ librariesLex }};

    // Add marker color, symbol, and size to hospital GeoJSON
    for (var i = 0; i < hospitals.features.length; i++) {
      hospitals.features[i].properties['marker-color'] = '#DC143C';
      hospitals.features[i].properties['marker-symbol'] = 'hospital';
      hospitals.features[i].properties['marker-size'] = 'small';
    }

    // Add marker color, symbol, and size to library GeoJSON
    for (var j = 0; j < libraries.features.length; j++) {
      libraries.features[j].properties['marker-color'] = '#4169E1';
      libraries.features[j].properties['marker-symbol'] = 'library';
      libraries.features[j].properties['marker-size'] = 'small';
    }

    var map = L.mapbox.map('map')
      .setView([38.05, -84.5], 12)
      .addLayer(L.mapbox.styleLayer('mapbox://styles/mapbox/light-v10'));
    map.scrollWheelZoom.disable();

    var hospitalLayer = L.mapbox.featureLayer(hospitals)
      .addTo(map);
    var libraryLayer = L.mapbox.featureLayer(libraries)
      .addTo(map);

    map.fitBounds(libraryLayer.getBounds());

    // Bind a popup to each feature in hospitalLayer and libraryLayer
    hospitalLayer.eachLayer(function(layer) {
      layer.bindPopup('<strong>' + layer.feature.properties.Name + '</strong>', { closeButton: false });
    }).addTo(map);
    libraryLayer.eachLayer(function(layer) {
      layer.bindPopup(layer.feature.properties.Name, { closeButton: false });
    }).addTo(map);

    // Open popups on hover
    libraryLayer.on('mouseover', function(e) {
      e.layer.openPopup();
    });
    hospitalLayer.on('mouseover', function(e) {
      e.layer.openPopup();
    });

    // Reset marker size to small
    function reset() {
      var hospitalFeatures = hospitalLayer.getGeoJSON();
      for (var k = 0; k < hospitalFeatures.features.length; k++) {
        hospitalFeatures.features[k].properties['marker-size'] = 'small';
      }
      hospitalLayer.setGeoJSON(hospitalFeatures);
    }

    // When a library is clicked, do the following
    libraryLayer.on('click', function(e) {
      // Reset any and all marker sizes to small
      reset();
      // Get the GeoJSON from libraryFeatures and hospitalFeatures
      var libraryFeatures = libraryLayer.getGeoJSON();
      var hospitalFeatures = hospitalLayer.getGeoJSON();
      // Using Turf, find the nearest hospital to library clicked
      var nearestHospital = turf.nearest(e.layer.feature, hospitalFeatures);
      // Change the nearest hospital to a large marker
      nearestHospital.properties['marker-size'] = 'large';
      // Add the new GeoJSON to hospitalLayer
      hospitalLayer.setGeoJSON(hospitalFeatures);
      // Bind popups to new hospitalLayer and open popup
      // for nearest hospital
      hospitalLayer.eachLayer(function(layer) {
        layer.bindPopup('<strong>' + layer.feature.properties.Name + '</strong>', { closeButton: false });
        if (layer.feature.properties['marker-size'] === 'large') {
          layer.openPopup();
        }
      });
    });

    // When the map is clicked on anywhere, reset all
    // hospital markers to small
    map.on('click', function(e) {
      reset();
    });

  </script>
</body>
</html>
```

## Next steps

[Turf](http://turfjs.org) has dozens of tools that would help extend this map even further. For example, you could also use [turf.distance](http://turfjs.org/docs/#distance) to determine not only which hospital is closest, but exactly how far away it is. The possibilities are virtually endless with Turf.js!
