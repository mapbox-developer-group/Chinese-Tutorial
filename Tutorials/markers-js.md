---
title: Work with markers in Mapbox.js
description: Add custom, interactive markers to your map with Mapbox.js.
thumbnail: markersJs
level: 2
topics:
- web apps
legacy: true
prependJs:
  - "import * as constants from '../../constants';"
  - "import { LegacyNote } from '../../components/legacy-note';"
  - "import { DemoStatic } from '../../components/demo-static';"
contentType: tutorial
language:
- JavaScript
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

In this guide, we’ll show how to add [markers](/help/glossary/marker/), customize them, and make them interactive with Mapbox.js. Think of this guide as a curated stroll through all that’s possible with markers in Mapbox.js.

## Getting started

For this guide you'll need **your API access token.** You can find your access token on your [Account page](https://www.mapbox.com/account/). To better understand each example, you can copy the full source code into your own local project and experiment. We adapted many of these demos from [Mapbox.js examples](https://www.mapbox.com/mapbox.js/example/v1.0.0/).

## Add markers

You can add markers to your map using [Leaflet](http://leafletjs.com/) or with GeoJSON using Mapbox.js.

### Add markers in Leaflet

You can add a DOM marker to your map with [L.marker](https://www.mapbox.com/mapbox.js/api/{{constants.VERSION_MAPBOXJS}}/l-marker/). In the example below, we added a marker to the map by knowing its coordinates. Use this technique when you have only a few markers to add.

```html
<div id='map-leaflet' class='map'> </div>
<script>
var mapLeaflet = L.mapbox.map('map-leaflet')
  .setView([37.8, -96], 4)
  .addLayer(L.mapbox.styleLayer('mapbox://styles/mapbox/light-v10'));

L.marker([38.913184, -77.031952]).addTo(mapLeaflet);
L.marker([37.775408, -122.413682]).addTo(mapLeaflet);

mapLeaflet.scrollWheelZoom.disable();
</script>
```

### Add markers with GeoJSON in Mapbox.js

You can also save your marker coordinates as [GeoJSON](/help/glossary/geojson/) and then load your GeoJSON on a map with Mapbox.js. In this example, we added the coordinates of the Mapbox D.C. and San Francisco offices to our inline GeoJSON. The GeoJSON format organizes features, especially when working with larger data files.

```html
<div id='map_geo' class='map'> </div>
<script>
var geojson = [
  {
    type: 'Feature',
    geometry: {
      type: 'Point',
      coordinates: [-77.031952, 38.913184]
    }
  },
  {
    type: 'Feature',
    geometry: {
      type: 'Point',
      coordinates: [-122.413682, 37.775408]
    }
  }
];

var mapGeo = L.mapbox.map('map_geo')
  .setView([37.8, -96], 4)
  .addLayer(L.mapbox.styleLayer('mapbox://styles/mapbox/light-v10'));

var myLayer = L.mapbox.featureLayer().setGeoJSON(geojson).addTo(mapGeo);
mapGeo.scrollWheelZoom.disable();
</script>
```

You can also load GeoJSON as an external file [hosted locally](https://www.mapbox.com/mapbox.js/example/v1.0.0/geojson-marker-from-url/) or on [GitHub](https://www.mapbox.com/mapbox.js/example/v1.0.0/geojson-marker-from-remote-url/). In the next section, you'll learn how to style GeoJSON markers with the [simplestyle specification](/help/glossary/simplestyle/).

If you're new to working with GeoJSON, here are some tools to help you generate, validate, or format GeoJSON:

- [geojson.net](https://geojson.net) &mdash; create and customize GeoJSON.
- [`geojsonhint`](https://github.com/mapbox/geojsonhint) &mdash; validate GeoJSON with this lint tool.
- [toGeoJSON](http://mapbox.github.io/togeojson/) &mdash; convert a KML or GPX file to GeoJSON.
- [csv2geojson](http://mapbox.github.io/csv2geojson/) &mdash; convert a CSV file to GeoJSON.

## Style markers

To style a marker, you can add [simplestyle](/help/glossary/simplestyle/) to your GeoJSON, load a custom image, or create your own markers with HTML and CSS.

### Style markers with simplestyle

The [simplestyle spec](/help/glossary/simplestyle) is a styling convention for GeoJSON. This means that you can add specific keys and values to each marker to change a marker's color, symbol, and size.

Here are all the styling options available as keys and values:

Key                | Value                 | Example
------------------|------------------------|----------------
`"marker-color"`  | Any hex value<br>Example: `"#3bb2d0"` |  {{ <DemoStatic src="https://api.mapbox.com/v4/mapbox.light/pin-m+3bb2d0(-73.975,40.767)/auto/80x100@2x.png?access_token=MapboxAccessToken" alt="Blue-colored marker" width="80" /> }}
`"marker-symbol"` | Any [Maki icon name](https://labs.mapbox.com/maki-icons), an integer, or a lowercase letter<br> Example: `"1"` | {{ <DemoStatic src="https://api.mapbox.com/v4/mapbox.light/pin-m-1+3bb2d0(-73.975,40.767)/auto/80x100@2x.png?access_token=MapboxAccessToken" alt="marker with '1' symbol" width="80" /> }}
`"marker-size"`   | small, medium, large<br>Example: `"large"` | {{ <DemoStatic src="https://api.mapbox.com/v4/mapbox.light/pin-l-1+3bb2d0(-73.975,40.767)/auto/80x100@2x.png?access_token=MapboxAccessToken" alt="large marker" width="80" /> }}

In this example, we took the [GeoJSON from the previous section](#add-markers-with-geojson-in-mapboxjs) and added simplestyle. View the source to see how the marker styles are added to each feature.

```html
<div id='map_simple' class='map'> </div>
<script>
var geojson = [
  {
    type: 'Feature',
    geometry: {
      type: 'Point',
      coordinates: [-77.031952, 38.913184]
    },
    properties: {
      'marker-color': '#3bb2d0',
      'marker-size': 'large',
      'marker-symbol': 'rocket'
    }
  },
  {
    type: 'Feature',
    geometry: {
      type: 'Point',
      coordinates: [-122.413682, 37.775408]
    },
    properties: {
      'marker-color': '#3bb2d0',
      'marker-size': 'large',
      'marker-symbol': 'rocket'
    }
  }
];

var mapSimple = L.mapbox.map('map_simple')
  .setView([37.8, -96], 4)
  .addLayer(L.mapbox.styleLayer('mapbox://styles/mapbox/light-v10'));
var myLayer = L.mapbox.featureLayer().setGeoJSON(geojson).addTo(mapSimple);
mapSimple.scrollWheelZoom.disable();
</script>
```

### Style markers with an image

You can define a custom marker image in your GeoJSON by adding an `icon` object to each feature's `properties`. In this example, [L.icon](https://www.mapbox.com/mapbox.js/api/{{constants.VERSION_MAPBOXJS}}/l-icon/) is used to set the marker image to each feature's `iconURL`.

```html
<div id='map-one' class='map'> </div>
<script>
var mapOne = L.mapbox.map('map-one')
  .setView([37.8, -96], 4)
  .addLayer(L.mapbox.styleLayer('mapbox://styles/mapbox/light-v10'));
var myLayer = L.mapbox.featureLayer().addTo(mapOne);

var geojson = [
  {
    type: 'Feature',
    geometry: {
      type: 'Point',
      coordinates: [-77.031952, 38.913184]
    },
    properties: {
      icon: {
        iconUrl: 'https://www.mapbox.com/mapbox.js/assets/images/astronaut1.png',
        iconSize: [50, 50], // size of the icon
        iconAnchor: [25, 25], // point of the icon which will correspond to marker's location
        popupAnchor: [0, -25], // point from which the popup should open relative to the iconAnchor
        className: 'dot'
      }
    }
  },
  {
    type: 'Feature',
    geometry: {
      type: 'Point',
      coordinates: [-122.413682, 37.775408]
    },
    properties: {
      icon: {
        iconUrl: 'https://www.mapbox.com/mapbox.js/assets/images/astronaut2.png',
        iconSize: [50, 50], // size of the icon
        iconAnchor: [25, 25], // point of the icon which will correspond to marker's location
        popupAnchor: [0, -25], // point from which the popup should open relative to the iconAnchor
        className: 'dot'
      }
    }
  }
];
myLayer.on('layeradd', function(e) {
  var marker = e.layer,
    feature = marker.feature;
  marker.setIcon(L.icon(feature.properties.icon));
});
myLayer.setGeoJSON(geojson);
mapOne.scrollWheelZoom.disable();
</script>
```

### Style markers with HTML and CSS

If you'd like to customize your markers even more, you can replace the standard marker with a `<div>`, assign it a class, and then style it with CSS using [L.divIcon](https://www.mapbox.com/mapbox.js/api/{{constants.VERSION_MAPBOXJS}}/l-divicon/). In this example, you'll follow a similar pattern as you did when adding a [marker image](#style-markers-with-an-image), but instead you'll assign a class name to the features and then add CSS to style it.

```html
<style>
.my-icon {
  border-radius: 100%;
  width: 20px;
  height: 20px;
  text-align: center;
  line-height: 20px;
  color: white;
}

.icon-dc {
  background: #3bb2d0;
}

.icon-sf {
  background: #3bb2d0;
}
</style>
<div id='map-two' class='map'> </div>
<script>
var mapTwo = L.mapbox.map('map-two')
  .setView([37.8, -96], 4)
  .addLayer(L.mapbox.styleLayer('mapbox://styles/mapbox/light-v10'));

var myLayer = L.mapbox.featureLayer().addTo(mapTwo);

var geojson = [
  {
    type: 'Feature',
    geometry: {
      type: 'Point',
      coordinates: [-77.031952, 38.913184]
    },
    properties: {
      icon: {
        className: 'my-icon icon-dc', // class name to style
        html: '&#9733;', // add content inside the marker, in this case a star
        iconSize: null // size of icon, use null to set the size in CSS
      }
    }
  },
  {
    type: 'Feature',
    geometry: {
      type: 'Point',
      coordinates: [-122.413682, 37.775408]
    },
    properties: {
      icon: {
        className: 'my-icon icon-sf', // class name to style
        html: '&#9733;', // add content inside the marker, in this case a star
        iconSize: null // size of icon, use null to set the size in CSS
      }
    }
  }
];
myLayer.on('layeradd', function(e) {
  var marker = e.layer,
    feature = marker.feature;
  marker.setIcon(L.divIcon(feature.properties.icon));
});
myLayer.setGeoJSON(geojson);

mapTwo.scrollWheelZoom.disable();
</script>
```html

## Add popups

You can add popups with simplestyle in your GeoJSON or with JavaScript.

### Add popups with simplestyle

Simplestyle allows you to add popups automatically if you add `title` and `description` keys to each feature's properties. In the example below, these fields are added to the GeoJSON. Click the markers to trigger the popup.

```html
<div id='map-popups' class='map'> </div>
<script>
var mapPopups = L.mapbox.map('map-popups')
  .setView([37.8, -96], 4)
  .addLayer(L.mapbox.styleLayer('mapbox://styles/mapbox/light-v10'));
var myLayer = L.mapbox.featureLayer().addTo(mapPopups);

var geojson = [
  {
    type: 'Feature',
    geometry: {
      type: 'Point',
      coordinates: [-77.031952, 38.913184]
    },
    properties: {
      title: 'Mapbox DC',
      description: '1714 14th St NW, Washington DC',
      'marker-color': '#3bb2d0',
      'marker-size': 'large',
      'marker-symbol': 'rocket'
    }
  },
  {
    type: 'Feature',
    geometry: {
      type: 'Point',
      coordinates: [-122.413682, 37.775408]
    },
    properties: {
      title: 'Mapbox SF',
      description: '155 9th St, San Francisco',
      'marker-color': '#3bb2d0',
      'marker-size': 'large',
      'marker-symbol': 'rocket'
    }
  }
];
myLayer.setGeoJSON(geojson);
mapPopups.scrollWheelZoom.disable();
</script>
```

You can add HTML to you popups by adding it to the `title` and `description` values in your GeoJSON. This allows you to add links, images, videos, lists, and other HTML elements to your popups.

### Add popups with JavaScript

You can customize the content of each popup with the [L.bindPopup](https://www.mapbox.com/mapbox.js/api/{{constants.VERSION_MAPBOXJS}}/l-popup/) method. In this example, an `image` key is added to each feature's property object, and a reference to this key when is included when `bindPopup()` is called to make the image appear inside the popup.

```html
<div id='map-popups-js' class='map'> </div>
<script>
var mapPopupsJS = L.mapbox.map('map-popups-js')
  .setView([37.8, -96], 4)
  .addLayer(L.mapbox.styleLayer('mapbox://styles/mapbox/light-v10'));
var myLayer = L.mapbox.featureLayer().addTo(mapPopupsJS);

var geojson = [
  {
    type: 'Feature',
    geometry: {
      type: 'Point',
      coordinates: [-77.031952, 38.913184]
    },
    properties: {
      title: 'Mapbox DC',
      description: '1714 14th St NW, Washington DC',
      image: 'https://farm9.staticflickr.com/8604/15769066303_3e4dcce464_n.jpg',
      icon: {
        iconUrl: 'https://www.mapbox.com/mapbox.js/assets/images/astronaut1.png',
        iconSize: [50, 50], // size of the icon
        iconAnchor: [25, 25], // point of the icon which will correspond to marker's location
        popupAnchor: [0, -25], // point from which the popup should open relative to the iconAnchor
        className: 'dot'
      }
    }
  },
  {
    type: 'Feature',
    geometry: {
      type: 'Point',
      coordinates: [-122.413682, 37.775408]
    },
    properties: {
      title: 'Mapbox SF',
      description: '155 9th St, San Francisco',
      image: 'https://farm9.staticflickr.com/8571/15844010757_63b093d527_n.jpg',
      icon: {
        iconUrl: 'https://www.mapbox.com/mapbox.js/assets/images/astronaut2.png',
        iconSize: [50, 50], // size of the icon
        iconAnchor: [25, 25], // point of the icon which will correspond to marker's location
        popupAnchor: [0, -25], // point from which the popup should open relative to the iconAnchor
        className: 'dot'
      }
    }
  }
];

// Set a custom icon on each marker based on feature properties.
myLayer.on('layeradd', function(e) {
  var marker = e.layer,
    feature = marker.feature;
  marker.setIcon(L.icon(feature.properties.icon));
  var content = '<p><strong>' + feature.properties.title + '</strong></p><img src="' + feature.properties.image + '" alt="">';
  marker.bindPopup(content);
});
myLayer.setGeoJSON(geojson);
mapPopupsJS.scrollWheelZoom.disable();
</script>
```

### More examples

You can further customize your popups with Mapbox.js. Here are more examples to get you started:

* [Add an image gallery to a popup](https://www.mapbox.com/mapbox.js/example/v1.0.0/markers-with-image-slideshow/)
* [Show popup outside of the marker](https://www.mapbox.com/mapbox.js/example/v1.0.0/marker-tooltips-outside-map/)
* [Embed a video in a popup](https://www.mapbox.com/mapbox.js/example/v1.0.0/video/)
* [Embed an audio clip in a popup](https://www.mapbox.com/mapbox.js/example/v1.0.0/soundcloud-embed/)
* [Tabs in popups](https://www.mapbox.com/mapbox.js/example/v1.0.0/marker-tooltip-tab-groups/)
* [Style popups with CSS](https://www.mapbox.com/mapbox.js/example/v1.0.0/custom-popup-style/)

## Cluster markers

For dense point data, try the Leaflet plug-in Markercluster to visualize your data. In the example below, we load an external GeoJSON file, create a `clustergroup` from the data, and add it to the map. Since Markercluster is a plugin, you'll need to add [additional CSS and JS](https://www.mapbox.com/mapbox.js/plugins/#leaflet-markercluster) to enable it.

```html
<script src='https://api.mapbox.com/mapbox.js/plugins/leaflet-markercluster/{{constants.VERSION_MAPBOXJS}}/leaflet.markercluster.js'></script>
<link href='https://api.mapbox.com/mapbox.js/plugins/leaflet-markercluster/{{constants.VERSION_MAPBOXJS}}/MarkerCluster.css' rel='stylesheet' />
<link href='https://api.mapbox.com/mapbox.js/plugins/leaflet-markercluster/{{constants.VERSION_MAPBOXJS}}/MarkerCluster.Default.css' rel='stylesheet' />
<div id='map-cluster' class='map'></div>
<script>
var mapCluster = L.mapbox.map('map-cluster')
  .setView([38.9, -77], 11)
  .addLayer(L.mapbox.styleLayer('mapbox://styles/mapbox/light-v10'));
L.mapbox.featureLayer()
  .loadURL('/help/data/stations.geojson')
  .on('ready', function(e) {
    var clusterGroup = new L.MarkerClusterGroup();
    e.target.eachLayer(function(layer) {
      clusterGroup.addLayer(layer);
    });
    mapCluster.addLayer(clusterGroup);
  });
mapCluster.scrollWheelZoom.disable();
</script>
```

### More examples

For more ideas of what you can do with clusters in Mapbox.js, explore these examples:

* [Marker clusters with Mapbox data](https://www.mapbox.com/mapbox.js/example/v1.0.0/markercluster-with-mapbox-data/)
* [Multiple differently styled clusters](https://www.mapbox.com/mapbox.js/example/v1.0.0/markercluster-multiple-groups/)
* [Clusters with custom polygon appearance](https://www.mapbox.com/mapbox.js/example/v1.0.0/markercluster-custom-polygon-appearance/)
* [Clusters with custom cluster icons](https://www.mapbox.com/mapbox.js/example/v1.0.0/markercluster-custom-marker-icons/)

## Toggle layers

Finally, take a look at how to toggle layers in Mapbox.js. You can help users sift through your markers by adding filters to let them turn layers on and off. In this example, the script automatically creates a toggle option for each transit line and will only add a new layer to the toggle list if its `line` is declared in the GeoJSON.

```html
<style>
.filter-ui {
  background: #fff;
  position: absolute;
  top: 10px;
  right: 10px;
  z-index: 100;
  padding: 10px;
  border-radius: 3px;
}

.filter-ui input {
  vertical-align: middle;
}
</style>
<nav id='filters' class='filter-ui'></nav>
<div id='map-toggle' class='map'></div>
<script>

var mapToggle = L.mapbox.map('map-toggle')
  .setView([38.9, -77], 11)
  .addLayer(L.mapbox.styleLayer('mapbox://styles/mapbox/light-v10'));

var filters = document.getElementById('filters');

var markers = L.mapbox.featureLayer().loadURL('/help/data/examples/stations.geojson');

markers.on('ready', function(e) {
  var typesObj = {},
    types = [];
  var features = e.target._geojson.features;
  for (var i = 0; i < features.length; i++) {
    typesObj[features[i].properties.line] = true;
  }
  for (var key in typesObj) {
    if ({}.hasOwnProperty.call(typesObj, key)) {
      types.push(key);
    }
  }
  var checkboxes = [];
  for (var j = 0; j < types.length; j++) {
    var item = filters.appendChild(document.createElement('div'));
    var checkbox = item.appendChild(document.createElement('input'));
    var label = item.appendChild(document.createElement('label'));
    checkbox.type = 'checkbox';
    checkbox.id = types[j];
    checkbox.checked = true;
    label.innerHTML = types[j];
    label.setAttribute('for', types[j]);
    checkbox.addEventListener('change', update);
    checkboxes.push(checkbox);
  }

  function update() {
    var enabled = {};
    for (var k = 0; k < checkboxes.length; k++) {
      if (checkboxes[k].checked) enabled[checkboxes[k].id] = true;
    }
    markers.setFilter(function(feature) {
      return feature.properties.line in enabled;
    });
  }
}).addTo(mapToggle);
mapToggle.scrollWheelZoom.disable();
</script>
```

### More examples

For more ideas on how to filter or toggle your markers, explore these examples:

- [Filter by marker symbol](https://www.mapbox.com/mapbox.js/example/v1.0.0/multiple-marker-filters/)
- [Multiple filters on markers](https://www.mapbox.com/mapbox.js/example/v1.0.0/markers-with-multiple-filters/)
- [Toggling layers](https://www.mapbox.com/mapbox.js/example/v1.0.0/layers/)

## Next steps

You now have the tools, code, and inspiration to add any markers you need to your map. For more ways to extend your Mapbox.js project, explore the [Build a store locator](/help/tutorials/building-a-store-locator-js/) tutorial.
