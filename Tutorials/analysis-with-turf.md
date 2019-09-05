---
title: Analyze data with Turf.js and Mapbox GL JS
description: Using Turf.js, add spatial analysis to our map to solve problems. This guide walks through an example of Turf.js and Mapbox GL JS in a real-world context.
thumbnail: analysisWithTurf
level: 2
topics:
- web apps
- analysis
language:
- JavaScript
prereq: Familiarity with front-end development concepts.
prependJs:
  - "import * as constants from '../../constants';"
  - "import UserAccessToken from '../../components/user-access-token';"
  - "import DemoIframe from '@mapbox/dr-ui/demo-iframe';"
contentType: tutorial
---

This guide walks through the basics of [Turf.js](http://turfjs.org), a JavaScript library for spatial analysis and statistics, and how to use it to add spatial analysis to your Mapbox GL JS maps.

Let's say you are part of a team that manages health and safety for the libraries in Lexington, KY. One important part of your preparedness mandate is to know __which hospital is closest to each library__ in case there's an emergency at one of your facilities. This example will walk you through making a map of libraries and hospitals; when a user clicks on a library, the map will show which hospital is nearest.

{{
  <DemoIframe src="/help/demos/turfjs-intro/demo-four.html" />
}}

## Getting started

There are a few resources you'll need to get started:

- [__An access token__](/help/glossary/access-token/). The token is used to associate a map with your account. You can find your access tokens on your [Access Tokens page](https://www.mapbox.com/account/access-tokens/) and below:

```js
mapboxgl.accessToken = '{{ <UserAccessToken /> }}';
```

- [__Mapbox GL JS__](https://www.mapbox.com/mapbox-gl-js/). A Mapbox JavaScript API for building maps.
- [__Turf.js__](http://turfjs.org/). Turf is the JavaScript library you'll be using today to add analysis to your map.
- __Data.__ This example uses two data files: hospitals in Lexington, KY and libraries in Lexington, KY.
- __A text editor.__ You'll be writing HTML, CSS, and JavaScript.

## Add structure

For this guide, include the latest versions of Mapbox GL JS and Turf.js. Add these libraries to your HTML file by copying the snippet below.

```html
<link href='https://api.mapbox.com/mapbox-gl-js/{{constants.VERSION_MAPBOXGLJS}}/mapbox-gl.css' rel='stylesheet' />
<script src='https://api.mapbox.com/mapbox-gl-js/{{constants.VERSION_MAPBOXGLJS}}/mapbox-gl.js'></script>
<script src='https://api.mapbox.com/mapbox.js/plugins/turf/{{constants.VERSION_TURF}}/turf.min.js'></script>
```

Now, add your map element. First, in the `body`, create an empty `div` for your map.

```html
<div id='map'></div>
```

Next, add some CSS to a `style` element in the `head` so your map takes up the width of the page.

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

Now that your page has some nice structure to it, go ahead and get a map on the page using Mapbox GL JS. This is where you'll need to use your access token. Add the following script inside the `<body>` after the HTML. Create a `new mapboxgl.Map` object called `map`. In this example, you'll be using the Mapbox Light template style, but you could also use a [custom style made with Mapbox Studio](/help/tutorials/create-a-custom-style). Finally, use `center` and `zoom` to set the view on Lexington, KY.

```js
mapboxgl.accessToken = '{{ <UserAccessToken /> }}';
var map = new mapboxgl.Map({
  container: 'map', // container id
  style: 'mapbox://styles/mapbox/light-v{{constants.VERSION_LIGHT_STYLE}}', // stylesheet location
  center: [-84.5, 38.05], // starting position
  zoom: 12 // starting zoom
});
```

Sweet! Now your page has a map centered on Lexington, KY.

{{
  <DemoIframe src="/help/demos/turfjs-intro/demo-one.html" />
}}


## Load data

As mentioned above, this example uses two data files: libraries and hospitals in Lexington, KY, each of them is a GeoJSON FeatureCollection. In the next step, you'll add them to the style as layers and add code to make sure they're styled differently from each other.

```js
var hospitals = {
  type: 'FeatureCollection',
  features: [
    { type: 'Feature', properties: { Name: 'VA Medical Center -- Leestown Division', Address: '2250 Leestown Rd' }, geometry: { type: 'Point', coordinates: [-84.539487, 38.072916] } },
    { type: 'Feature', properties: { Name: 'St. Joseph East', Address: '150 N Eagle Creek Dr' }, geometry: { type: 'Point', coordinates: [-84.440434, 37.998757] } },
    { type: 'Feature', properties: { Name: 'Central Baptist Hospital', Address: '1740 Nicholasville Rd' }, geometry: { type: 'Point', coordinates: [-84.512283, 38.018918] } },
    { type: 'Feature', properties: { Name: 'VA Medical Center -- Cooper Dr Division', Address: '1101 Veterans Dr' }, geometry: { type: 'Point', coordinates: [-84.506483, 38.02972] } },
    { type: 'Feature', properties: { Name: 'Shriners Hospital for Children', Address: '1900 Richmond Rd' }, geometry: { type: 'Point', coordinates: [-84.472941, 38.022564] } },
    { type: 'Feature', properties: { Name: 'Eastern State Hospital', Address: '627 W Fourth St' }, geometry: { type: 'Point', coordinates: [-84.498816, 38.060791] } },
    { type: 'Feature', properties: { Name: 'Cardinal Hill Rehabilitation Hospital', Address: '2050 Versailles Rd' }, geometry: { type: 'Point', coordinates: [-84.54212, 38.046568] } },
    { type: 'Feature', properties: { Name: 'St. Joseph Hospital', ADDRESS: '1 St Joseph Dr' }, geometry: { type: 'Point', coordinates: [-84.523636, 38.032475] } },
    { type: 'Feature', properties: { Name: 'UK Healthcare Good Samaritan Hospital', Address: '310 S Limestone' }, geometry: { type: 'Point', coordinates: [-84.501222, 38.042123] } },
    { type: 'Feature', properties: { Name: 'UK Medical Center', Address: '800 Rose St' }, geometry: { type: 'Point', coordinates: [-84.508205, 38.031254] } }
  ]
};
var libraries = {
  type: 'FeatureCollection',
  features: [
    { type: 'Feature', properties: { Name: 'Village Branch', Address: '2185 Versailles Rd' }, geometry: { type: 'Point', coordinates: [-84.548369, 38.047876] } },
    { type: 'Feature', properties: { Name: 'Northside Branch', ADDRESS: '1733 Russell Cave Rd' }, geometry: { type: 'Point', coordinates: [-84.47135, 38.079734] } },
    { type: 'Feature', properties: { Name: 'Central Library', ADDRESS: '140 E Main St' }, geometry: { type: 'Point', coordinates: [-84.496894, 38.045459] } },
    { type: 'Feature', properties: { Name: 'Beaumont Branch', Address: '3080 Fieldstone Way' }, geometry: { type: 'Point', coordinates: [-84.557948, 38.012502] } },
    { type: 'Feature', properties: { Name: 'Tates Creek Branch', Address: '3628 Walden Dr' }, geometry: { type: 'Point', coordinates: [-84.498679, 37.979598] } },
    { type: 'Feature', properties: { Name: 'Eagle Creek Branch', Address: '101 N Eagle Creek Dr' }, geometry: { type: 'Point', coordinates: [-84.442219, 37.999437] } }
  ]
};

map.on('load', function() {
  map.addLayer({
    id: 'hospitals',
    type: 'symbol',
    source: {
      type: 'geojson',
      data: hospitals
    },
    layout: {
      'icon-image': 'hospital-15',
      'icon-allow-overlap': true
    },
    paint: { }
  });
  map.addLayer({
    id: 'libraries',
    type: 'symbol',
    source: {
      type: 'geojson',
      data: libraries
    },
    layout: {
      'icon-image': 'library-15'
    },
    paint: { }
  });
});
```

Note that `hospitals` layer and `libraries` layer are added to the map _after_ the map by wrapping them in `map.on('load', function(){});`

{{
  <DemoIframe src="/help/demos/turfjs-intro/demo-two.html" />
}}

## Add interactivity

Your map users will want to know the names of the libraries and hospitals displayed on the map, so next you'll add some popups. For this map, add some popups to these features that appear when the user hovers over the markers. Insert this into your script after you've created `hospitals` layer and `libraries` layer.

```js
var popup = new mapboxgl.Popup();

map.on('mousemove', function(e) {
  var features = map.queryRenderedFeatures(e.point, { layers: ['hospitals', 'libraries'] });
  if (!features.length) {
    popup.remove();
    return;
  }
  var feature = features[0];

  popup.setLngLat(feature.geometry.coordinates)
    .setHTML(feature.properties.Name)
    .addTo(map);

  map.getCanvas().style.cursor = features.length ? 'pointer' : '';
});
```

Next you'll make your map of the libraries and hospitals in Lexington even more useful by adding some analysis.

{{
  <DemoIframe src="/help/demos/turfjs-intro/demo-three.html" />
}}

## Add Turf

[Turf](http://turfjs.org) is a JavaScript library for adding spatial and statistical analysis to your web maps. It contains many commonly-used GIS tools -- like buffer, union, and merge -- as well as statistical analysis functions -- like sum, median, and average.

Fortunately, Turf has some functions that will help you out here! You're going to update your map so that clicking on a library will show users which hospital is closest to that library.

As a first step, you'll need to add a new source with the id `'nearest-hospital'` when the map is loaded.

```js
map.addSource('nearest-hospital', {
  type: 'geojson',
  data: {
    type: 'FeatureCollection',
    features: [
    ]
  }
});
```
You’ll make an “event handler” for when someone clicks on a library marker. When an event occurs, like a click on a marker, the event handler tells the map what to do in response. Before, you created event handlers for hovering over hospital and library markers; now you’re going to make one for clicks.

This is the structure of an event handler; anything you want to happen on click goes inside of the braces `{}`. In this case, you want to use Turf to identify the nearest hospital to the clicked library and make that marker larger to identify it.

```js
map.on('click', function(e) {
  // Return any features from the 'libraries' layer whenever the map is clicked
  var libraryFeatures = map.queryRenderedFeatures(e.point, { layers: ['libraries'] });
  if (!libraryFeatures.length) {
    return;
  }
  var libraryFeature = libraryFeatures[0];

  // Using Turf, find the nearest hospital to library clicked
  var nearestHospital = turf.nearest(libraryFeature, hospitals);

  // If a nearest library is found
  if (nearestHospital !== null) {
    // Update the 'nearest-library' data source to include
    // the nearest library
    map.getSource('nearest-hospital').setData({
      type: 'FeatureCollection',
      features: [
        nearestHospital
      ]
    });
    // Create a new circle layer from the 'nearest-library' data source
    map.addLayer({
      id: 'nearest-hospital',
      type: 'circle',
      source: 'nearest-hospital',
      paint: {
        'circle-radius': 12,
        'circle-color': '#486DE0'
      }
    }, 'hospitals');
  }
});
```

{{
  <DemoIframe src="/help/demos/turfjs-intro/demo-four.html" />
}}

## Finished product

Nicely done! You have successfully created a map that calculates which hospital is closest to each library dynamically. Your finished HTML file should look like this:

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset='utf-8' />
    <title></title>
    <meta name='viewport' content='initial-scale=1,maximum-scale=1,user-scalable=no' />
    <script src='https://api.tiles.mapbox.com/mapbox-gl-js/{{constants.VERSION_MAPBOXGLJS}}/mapbox-gl.js'></script>
    <link href='https://api.tiles.mapbox.com/mapbox-gl-js/{{constants.VERSION_MAPBOXGLJS}}/mapbox-gl.css' rel='stylesheet' />
    <script src='https://npmcdn.com/@turf/turf/turf.min.js'></script>
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
  container: 'map', // container id
  style: 'mapbox://styles/mapbox/light-v{{constants.VERSION_LIGHT_STYLE}}', // stylesheet location
  center: [-84.5, 38.05], // starting position
  zoom: 11 // starting zoom
});

var hospitals = {
  type: 'FeatureCollection',
  features: [
    { type: 'Feature', properties: { Name: 'VA Medical Center -- Leestown Division', Address: '2250 Leestown Rd' }, geometry: { type: 'Point', coordinates: [-84.539487, 38.072916] } },
    { type: 'Feature', properties: { Name: 'St. Joseph East', Address: '150 N Eagle Creek Dr' }, geometry: { type: 'Point', coordinates: [-84.440434, 37.998757] } },
    { type: 'Feature', properties: { Name: 'Central Baptist Hospital', Address: '1740 Nicholasville Rd' }, geometry: { type: 'Point', coordinates: [-84.512283, 38.018918] } },
    { type: 'Feature', properties: { Name: 'VA Medical Center -- Cooper Dr Division', Address: '1101 Veterans Dr' }, geometry: { type: 'Point', coordinates: [-84.506483, 38.02972] } },
    { type: 'Feature', properties: { Name: 'Shriners Hospital for Children', Address: '1900 Richmond Rd' }, geometry: { type: 'Point', coordinates: [-84.472941, 38.022564] } },
    { type: 'Feature', properties: { Name: 'Eastern State Hospital', Address: '627 W Fourth St' }, geometry: { type: 'Point', coordinates: [-84.498816, 38.060791] } },
    { type: 'Feature', properties: { Name: 'Cardinal Hill Rehabilitation Hospital', Address: '2050 Versailles Rd' }, geometry: { type: 'Point', coordinates: [-84.54212, 38.046568] } },
    { type: 'Feature', properties: { Name: 'St. Joseph Hospital', Address: '1 St Joseph Dr' }, geometry: { type: 'Point', coordinates: [-84.523636, 38.032475] } },
    { type: 'Feature', properties: { Name: 'UK Healthcare Good Samaritan Hospital', Address: '310 S Limestone' }, geometry: { type: 'Point', coordinates: [-84.501222, 38.042123] } },
    { type: 'Feature', properties: { Name: 'UK Medical Center', Address: '800 Rose St' }, geometry: { type: 'Point', coordinates: [-84.508205, 38.031254] } }
  ]
};
var libraries = {
  type: 'FeatureCollection',
  features: [
    { type: 'Feature', properties: { Name: 'Village Branch', Address: '2185 Versailles Rd' }, geometry: { type: 'Point', coordinates: [-84.548369, 38.047876] } },
    { type: 'Feature', properties: { Name: 'Northside Branch', Address: '1733 Russell Cave Rd' }, geometry: { type: 'Point', coordinates: [-84.47135, 38.079734] } },
    { type: 'Feature', properties: { Name: 'Central Library', Address: '140 E Main St' }, geometry: { type: 'Point', coordinates: [-84.496894, 38.045459] } },
    { type: 'Feature', properties: { Name: 'Beaumont Branch', Address: '3080 Fieldstone Way' }, geometry: { type: 'Point', coordinates: [-84.557948, 38.012502] } },
    { type: 'Feature', properties: { Name: 'Tates Creek Branch', Address: '3628 Walden Dr' }, geometry: { type: 'Point', coordinates: [-84.498679, 37.979598] } },
    { type: 'Feature', properties: { Name: 'Eagle Creek Branch', Address: '101 N Eagle Creek Dr' }, geometry: { type: 'Point', coordinates: [-84.442219, 37.999437] } }
  ]
};


map.on('load', function() {
  map.addLayer({
    id: 'hospitals',
    type: 'symbol',
    source: {
      type: 'geojson',
      data: hospitals
    },
    layout: {
      'icon-image': 'hospital-15',
      'icon-allow-overlap': true
    },
    paint: { }
  });

  map.addLayer({
    id: 'libraries',
    type: 'symbol',
    source: {
      type: 'geojson',
      data: libraries
    },
    layout: {
      'icon-image': 'library-15'
    },
    paint: { }
  });

  map.addSource('nearest-hospital', {
    type: 'geojson',
    data: {
      type: 'FeatureCollection',
      features: []
    }
  });
});

var popup = new mapboxgl.Popup();

map.on('mousemove', function(e) {

  var features = map.queryRenderedFeatures(e.point, { layers: ['hospitals', 'libraries'] });
  if (!features.length) {
    popup.remove();
    return;
  }

  var feature = features[0];

  popup.setLngLat(feature.geometry.coordinates)
  .setHTML(feature.properties.Name)
  .addTo(map);

  map.getCanvas().style.cursor = features.length ? 'pointer' : '';

});

map.on('click', function(e) {
  var libraryFeatures = map.queryRenderedFeatures(e.point, { layers: ['libraries'] });
  if (!libraryFeatures.length) {
    return;
  }

  var libraryFeature = libraryFeatures[0];

  var nearestHospital = turf.nearest(libraryFeature, hospitals);

  if (nearestHospital !== null) {

    map.getSource('nearest-hospital').setData({
      type: 'FeatureCollection',
      features: [nearestHospital]
    });

    map.addLayer({
      id: 'nearest-hospital',
      type: 'circle',
      source: 'nearest-hospital',
      paint: {
        'circle-radius': 12,
        'circle-color': '#486DE0'
      }
    }, 'hospitals');
  }
});

</script>
</body>
</html>
```


## Next steps

[Turf](http://turfjs.org) has dozens of tools that would help extend this map even further. For example, you could also use [turf.distance](http://turfjs.org/docs#distance) to determine not only which hospital is closest, but exactly how far away it is. The possibilities are virtually endless with Turf.js!
