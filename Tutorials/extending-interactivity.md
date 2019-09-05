---
title: Extend with Mapbox.js
description: Meet Mapbox.js - the toolset for creating interactions and greater customization of your map and data.
thumbnail: extendingInteractivity
level: 2
topics:
- web apps
language:
- JavaScript
prereq: Familiarity with front-end development concepts.
legacy: true
prependJs:
  - "import * as constants from '../../constants';"
  - "import { LegacyNote } from '../../components/legacy-note';"
  - "import { geojsonSample } from '../../snippets/geojson-sample';"
  - "import UserAccessToken from '../../components/user-access-token';"
  - "import DemoIframe from '@mapbox/dr-ui/demo-iframe';"
contentType: tutorial
---

{{
  <LegacyNote
    legacyProduct='Mapbox.js'
    alternativeResource={{
      title: 'Add custom markers in Mapbox GL JS',
      link: '/help/tutorials/custom-markers-gl-js/'
    }}
  />
}}

This guide walks you through how to use [Mapbox.js](https://www.mapbox.com/mapbox.js/), a JavaScript API for rendering maps and creating custom interactions.

{{
  <DemoIframe gl={false} src="/help/demos/extending-interactivity/index.html" />
}}

## Getting started

For this guide you will need:

* **Your API access token.** If you're logged in, we automatically added your token to the examples in this guide. You can also find your access token on your [Account page](https://www.mapbox.com/account/).
* **A tileset ID.** You can use a [tileset ID](/help/glossary/tileset-id) from a default Mapbox Style or from your own Mapbox Studio Classic project. You can find your project's tileset ID by visiting your [Classic projects page](https://www.mapbox.com/studio/classic/projects/). It's not covered in this guide, but you can add a Mapbox Studio style to your Mapbox.js map by following [these instructions](https://www.mapbox.com/studio-manual/overview/publish-your-style/#mapboxjs).
* **Your favorite text editor**. You'll be writing some HTML and JavaScript, after all.

## Initialize a map

First, you'll need the latest version of Mapbox.js. You can link directly to the Mapbox-hosted version by copying this snippet into your HTML document:

```html
<script src='https://api.mapbox.com/mapbox.js/{{constants.VERSION_MAPBOXJS}}/mapbox.js'></script>
<link href='https://api.mapbox.com/mapbox.js/{{constants.VERSION_MAPBOXJS}}/mapbox.css' rel='stylesheet' />
```

To use a Mapbox map style with Mapbox.js, you also need a [style URL](/help/glossary/style-url/). We put a placeholder in for you, `mapbox://styles/mapbox/streets-v{{constants.VERSION_STREETS_STYLE}}`, but you can swap it out with the style URL for another Mapbox [map style](https://docs.mapbox.com/api/maps/#styles) or create your own custom style with [Mapbox Studio](https://docs.mapbox.com/studio-manual/).

```html
<div id='map' class='map'> </div>
<script>
<script>
var map = L.mapbox.map('map')
  .addLayer(L.mapbox.styleLayer('mapbox://styles/mapbox/streets-v11'));
</script>
```

### Coordinates

Now that you've loaded your map tiles, set the initial location and zoom level to show our map when the page is loaded. You can do this by adding `setView` to `L.map()` so that your map opens up to Washington, DC.

```html
<div id='map' class='map'> </div>
<script>
var map = L.mapbox.map('map')
  .setView([38.8929, -77.0252], 14)
  .addLayer(L.mapbox.styleLayer('mapbox://styles/mapbox/streets-v11'));
</script>
```

### Disable mouse zooming

Scrolling down a page that has a map can cause unwanted scroll zooming. For this guide, disable that interaction by setting `scrollWheelZoom` to false. Notice that you can't scroll zoom on the map anymore.

```html
<div id='map-three' class='map'> </div>
<script>
var map = L.mapbox.map('map')
  .setView([38.8929, -77.0252], 14)
  .addLayer(L.mapbox.styleLayer('mapbox://styles/mapbox/streets-v11'));
map.scrollWheelZoom.disable();  
</script>
```

## Add data

You can add data to our map to help tell a story, show a feature's location, or visualize a trend. Mapbox.js supports a few different formats, including [GeoJSON](/help/glossary/geojson), [KML](/help/glossary/kml), and [CSV](/help/glossary/csv). In this example, you'll start with GeoJSON.

### GeoJSON

GeoJSON is a format for storing geometric shapes and marker positions. Here's what a single point looks like in GeoJSON:

```json
{
  "type": "FeatureCollection",
  "features": [
    {
      "type": "Feature",
      "geometry": {
        "type": "Point",
        "coordinates": [
          -77.0366048812866,
          38.89784666877921
        ]
      },
      "properties": {}
    }
  ]
}
```

Does GeoJSON look like hieroglyphics to you? Don't sweat it. Once you learn the patterns, it becomes easier to write. If you need help, [geojson.net](http://geojson.net/) writes and displays GeoJSON for you.

### Add a marker

Store the GeoJSON as a variable called `geojson` and create a `featureLayer` to add it to the map.

```javascript
var myLayer = L.mapbox.featureLayer().addTo(map);
myLayer.setGeoJSON(geojson);
```

Now you have the marker on the map:

```html
<div id='map' class='map'> </div>
<script>
var geojson = {
  type: 'FeatureCollection',
  features: [
    {
      type: 'Feature',
      geometry: {
        type: 'Point',
        coordinates: [-77.0366048812866, 38.89784666877921]
      },
      properties: {}
    }
  ]
};
var map = L.mapbox.map('map')
  .setView([38.8929, -77.0252], 14)
  .addLayer(L.mapbox.styleLayer('mapbox://styles/mapbox/streets-v11'));
map.scrollWheelZoom.disable();  

var myLayer = L.mapbox.featureLayer().addTo(map);
myLayer.setGeoJSON(geojson);
</script>
```

If you have a lot of features, you'll want to move the GeoJSON to its own file. You can then load the GeoJSON [by specifying its URL](https://www.mapbox.com/mapbox.js/example/v1.0.0/geojson-marker-from-url/). You can also load a file from [a remote source like GitHub](https://www.mapbox.com/mapbox.js/example/v1.0.0/geojson-marker-from-remote-url/).

### Style data

The default gray style is rather boring, but you can customize it! You can specify your own styles within `"properties": {}` attribute found in the GeoJSON. Styles are defined according to [Simplestyle](https://github.com/mapbox/simplestyle-spec) rules. You can learn more about the supported property names by browsing the [specification](https://github.com/mapbox/simplestyle-spec/tree/master/1.1.0).

You can also add a `title` in the properties object to create a tooltip over the feature.

Here's what your GeoJSON looks like with styles and a title added to the marker:

```json
{
  "type": "FeatureCollection",
  "features": [
    {
      "type": "Feature",
      "geometry": {
        "type": "Point",
        "coordinates": [
          -77.0366048812866,
          38.89784666877921
        ]
      },
      "properties": {
        "title": "The White House",
        "marker-color": "#9c89cc",
        "marker-size": "medium",
        "marker-symbol": "building"
      }
    }
  ]
}
```

And here's the styled marker on the map:

```html
<div id='map' class='map'> </div>
<script>
var geojson = {
  type: 'FeatureCollection',
  features: [
    {
      type: 'Feature',
      geometry: {
        type: 'Point',
        coordinates: [-77.0366048812866, 38.89784666877921]
      },
      properties: {
        title: 'The White House',
        'marker-color': '#9c89cc',
        'marker-size': 'medium',
        'marker-symbol': 'building'
      }
    }
  ]
};
var map = L.mapbox.map('map')
  .setView([38.8929, -77.0252], 14)
  .addLayer(L.mapbox.styleLayer('mapbox://styles/mapbox/streets-v11'));
map.scrollWheelZoom.disable();  

var myLayer = L.mapbox.featureLayer().addTo(map);
myLayer.setGeoJSON(geojson);
</script>
```

Click on the marker to see the tooltip!

### Add a line

Make your map a little more interesting by adding *another* marker and a line to connect them.

Add a marker and line with set styles to our existing GeoJSON.

```json
{{geojsonSample}}
```

Here's how your new styled features look on the map:

```html
<div id='map' class='map'> </div>
<script>
var geojson = {{geojsonSample}};
var map = L.mapbox.map('map')
  .setView([38.8929, -77.0252], 14)
  .addLayer(L.mapbox.styleLayer('mapbox://styles/mapbox/streets-v11'));
map.scrollWheelZoom.disable();  

var myLayer = L.mapbox.featureLayer().addTo(map);
myLayer.setGeoJSON(geojson);
</script>
```

## Add a legend

Legends describe data on a map. Mapbox.js allows you to add a legend with `L.mapbox.legendControl.addLegend('Legend content')`. The `addLegend()` method takes HTML code as an argument, so feel free to customize your legend to fit your needs!

By default, legends appear at the bottom right of a map. Since you're working in a small space, nudge the legend up by setting `position: 'topright'` when the map is initialized.

The legend now appears on the map:

```html
<div id='map' class='map'> </div>
<script>
var geojson = {{geojsonSample}};

var map = L.mapbox.map('map')
  .setView([38.8929, -77.0252], 14)
  .addLayer(L.mapbox.styleLayer('mapbox://styles/mapbox/streets-v11'));
map.scrollWheelZoom.disable();

var myLayer = L.mapbox.featureLayer().addTo(map);
myLayer.setGeoJSON(geojson);

L.mapbox.legendControl({ position: 'topright' }).addLegend('<strong>My walk from the White House to the hill!</strong>').addTo(map);
</script>
```

## Finished product

You did it! This guide covered a lot and we hope you leave feeling equipped with skills and tools to build your own custom projects.

{{
  <DemoIframe gl={false} src="/help/demos/extending-interactivity/index.html" />
}}

## Next steps

Explore the [Mapbox.js examples](https://docs.mapbox.com/mapbox.js/examples/) page for more ideas and code to help you further customize your Mapbox.js projects.
