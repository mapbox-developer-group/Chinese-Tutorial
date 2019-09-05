---
title: Switch from Google Maps to Mapbox
description: Are you using the Google Maps API? This guide walks you through how to convert a Google web map to a Mapbox web map using Mapbox GL JS.
thumbnail: googleToMapbox
level: 2
topics:
- web apps
language:
- JavaScript
prereq: Familiarity with front-end development concepts.
prependJs:
  - "import * as constants from '../../constants';"
  - "import UserAccessToken from '../../components/user-access-token';"
  - "import DemoIframe from '@mapbox/dr-ui/demo-iframe';"
contentType: tutorial
---

Are you using Google Maps and want to switch to Mapbox? You’ve come to the right place! This tutorial will walk you through how to use [Mapbox GL JS](https://www.mapbox.com/mapbox-gl-js/api), a web mapping JavaScript library, to create a web map, add a [marker](/help/glossary/marker/), and attach a popup using similar methods that the Google Maps JavaScript API uses.

## Getting started

This guide assumes that you are already familiar with the Google Maps JavaScript API V3 and with front-end web development concepts including HTML, CSS, and JavaScript.

There are a few resources you'll need to get started:

- [__An access token__](/help/glossary/access-token/). The token is used to associate a map with your account.

```js
mapboxgl.accessToken = '{{ <UserAccessToken /> }}';
```

- [__Mapbox GL JS__](https://www.mapbox.com/mapbox-gl-js/). You’ll need the latest versions of the Mapbox GL JS JavaScript and CSS files. You can link directly to the Mapbox hosted versions by copying this snippet within the head tags of your HTML document.

```html
<script src='https://api.mapbox.com/mapbox-gl-js/{{constants.VERSION_MAPBOXGLJS}}/mapbox-gl.js'></script>
<link href='https://api.mapbox.com/mapbox-gl-js/{{constants.VERSION_MAPBOXGLJS}}/mapbox-gl.css' rel='stylesheet' />
```

- __A text editor.__ You'll be writing HTML, CSS, and JavaScript.

## Initializing a web map

First, set up an HTML file and add the above JavaScript and CSS files to the head. Once you've got your HTML file set up, head to the next step.

### Google

With the Google Maps JavaScript API, you can initialize a new map with JavaScript as shown below:

```js
var map = new google.maps.Map(document.getElementById('map'), {
  mapTypeId: 'roadmap',
  center: { lat: 64.1436456, lng: -21.9270884 },
  zoom: 13
});
```

### Mapbox GL JS

With Mapbox GL JS, you can initialize a map in a similar way. The result of the sample code below is a map that uses the Mapbox Streets template style, initialized at a set zoom level and coordinates. The `style` option below is set to the [style URL](/help/glossary/style-url/) for [Mapbox Streets](https://www.mapbox.com/maps/#styles), one of our template styles:


```js
var map = new mapboxgl.Map({
  container: 'map', // HTML container id
  style: 'mapbox://styles/mapbox/streets-v{{constants.VERSION_STREETS_STYLE}}', // style URL
  center: [-21.9270884, 64.1436456], // starting position as [lng, lat]
  zoom: 13
});
```

{{
  <DemoIframe src="/help/demos/google-to-mapbox/simple-map.html" />
}}

You can also use [custom styles](/help/tutorials/create-a-custom-style) created with Mapbox Studio, or you can [change your map's style dynamically](https://www.mapbox.com/mapbox-gl-js/api/#map#setstyle) in the browser at runtime, depending on your needs.

## Adding a marker

Now you're ready to add a single marker to your map.

### Google

With the Google Maps JavaScript API, you can add a marker to a map as shown below:

```js
var map = new google.maps.Map(document.getElementById('map'), {
  mapTypeId: 'roadmap',
  center: { lat: 64.1436456, lng: -21.9270884 },
  zoom: 13
});

var marker = new google.maps.Marker({
  position: { lat: 64.1436456, lng: -21.9270884 },
  title: 'Reykjavik Roasters - Coffee Shop',
  map: map
});
```

### Mapbox GL JS

There are many ways you can add [markers](/help/glossary/marker/) to a map in Mapbox GL JS. The example below uses our default marker:

```js
var map = new mapboxgl.Map({
  container: 'map', // HTML container id
  style: 'mapbox://styles/mapbox/streets-v{{constants.VERSION_STREETS_STYLE}}', // style URL
  center: [-21.9270884, 64.1436456], // starting position as [lng, lat]
  zoom: 13
});

var marker = new mapboxgl.Marker()
  .setLngLat([-21.9270884, 64.1436456])
  .addTo(map);
```

{{
  <DemoIframe src="/help/demos/google-to-mapbox/simple-marker.html" />
}}

You can also attach markers to a set of points by loading a [GeoJSON source](https://www.mapbox.com/mapbox-gl-js/example/geojson-line/) or a [vector tileset source](https://www.mapbox.com/mapbox-gl-js/example/vector-source).

## Adding interactivity

No marker is complete without a popup. In the next steps, add a popup that appears and displays information when the marker is clicked.

### Google

In the Google Maps JavaScript API, interactive popups are go by the name `InfoWindow` and are added like this:

```js
var map = new google.maps.Map(document.getElementById('map'), {
  mapTypeId: 'roadmap',
  center: { lat: 64.14356426, lng: -21.92661562 },
  zoom: 13
});

var marker = new google.maps.Marker({
  position: { lat: 64.14356426, lng: -21.92661562 },
  map: map
});

var infowindow = new google.maps.InfoWindow({
  content: '<h3>Reykjavik Roasters</h3><p>A good coffee shop</p>'
});

marker.addListener('click', function() {
  infowindow.open(map, marker);
});
```

### Mapbox GL JS

In Mapbox GL JS, you can attach the popup directly to the marker and it will be displayed when the marker is clicked by default. No need to add an event listener. Here's how you add a popup and populate it with some HTML content:

```js
var map = new mapboxgl.Map({
  container: 'map', // HTML container id
  style: 'mapbox://styles/mapbox/streets-v{{constants.VERSION_STREETS_STYLE}}', // style URL
  center: [-21.92661562, 64.14356426], // starting position as [lng, lat]
  zoom: 13
});

var popup = new mapboxgl.Popup()
  .setHTML('<h3>Reykjavik Roasters</h3><p>A good coffee shop</p>');

var marker = new mapboxgl.Marker()
  .setLngLat([-21.92661562, 64.14356426])
  .setPopup(popup)
  .addTo(map);
```

{{
  <DemoIframe src="/help/demos/google-to-mapbox/simple-popup.html" />
}}

## Next steps

You've made a web map with a marker and popup with Mapbox GL JS. Be sure to explore our other Mapbox GL JS tutorials for more ways to build on your map:

- [Add points to a web map](/help/tutorials/add-points-pt-1)
- [Create a custom style](/help/tutorials/create-a-custom-style)
- [Display map controls](https://www.mapbox.com/mapbox-gl-js/example/navigation/)
- [Mapbox Geocoding API](https://docs.mapbox.com/api/search/#geocoding)
- [Static maps](/help/how-mapbox-works/static-maps/)

Dive in further by checking out Mapbox GL JS [documentation](https://www.mapbox.com/mapbox-gl-js/api/) and [examples](https://www.mapbox.com/mapbox-gl-js/examples/)!
