---
title: Add custom markers in Mapbox GL JS
description: Add custom HTML markers, style them, and add tooltips with Mapbox GL JS.
thumbnail: customMarkersGlJs
level: 2
topics:
- web apps
language:
- JavaScript
prereq: Familiarity with front-end development concepts.
prependJs:
  - "import * as constants from '../../constants';"
  - "import Note from '@mapbox/dr-ui/note';"
  - "import BookImage from '@mapbox/dr-ui/book-image';"
  - "import Icon from '@mapbox/mr-ui/icon';"
  - "import UserAccessToken from '../../components/user-access-token';"
  - "import DemoIframe from '@mapbox/dr-ui/demo-iframe';"
  - "import Button from '@mapbox/mr-ui/button';"
contentType: tutorial
---

In this tutorial, you'll learn how to build an interactive web map with custom [markers](/help/glossary/marker/) using Mapbox GL JS, a JavaScript library that will require writing code. You'll learn how to load [GeoJSON](/help/glossary/geojson) data inline and add it to your map dynamically using HTML Markers. Finally, you'll add popups when a marker is clicked. Your final map will look like this:

{{
  <DemoIframe src="/help/demos/custom-markers-gl-js/index.html" />
}}

## Getting started

For this project, we recommend that you create a local folder called `mapbox-markers` to house your project files. You’ll see this folder referred to as your project folder.

To follow along with this guide you'll need:

- [__An access token__](/help/glossary/access-token/). from your account. You will use an access token to associate a map with your account. Your access token is on the [Account page](https://www.mapbox.com/account).
- **A text editor.** You'll be writing HTML, CSS, and JavaScript after all.
- **Custom image**. This tutorial uses an image within each custom HTML marker to show the location of the offices. You'll need to download the PNG file to use as your custom icon and save it in the same project folder as your index.html file.

{{
<Button href="/help/demos/custom-markers-gl-js/mapbox-icon.png" passthroughProps={{ download: "mapbox-icon" }} >
    <Icon name='arrow-down' inline={true} /> Download image
</Button>
}}

## Create a Mapbox GL JS map

Now you're ready to use Mapbox GL JS! To start, create a new HTML file and write code to initialize a Mapbox GL JS map.

### Initialize your map

1. Open your text editor.
1. Create a new HTML file.
1. Copy and paste the code below into your text editor to initialize your Mapbox GL JS map.
1. Make sure you are using your API access token with `mapboxgl.accessToken`.
1. Save your file as `index.html` in your project folder.
1. Open the file in a browser.
1. You should see an initialized Mapbox GL JS map displaying the Mapbox Light style in a browser window. You won't see your markers yet.

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset='utf-8' />
    <title></title>
    <meta name='viewport' content='initial-scale=1,maximum-scale=1,user-scalable=no' />
    <link href="https://fonts.googleapis.com/css?family=Open+Sans" rel="stylesheet">
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

mapboxgl.accessToken = '{{ <UserAccessToken /> }}';

var map = new mapboxgl.Map({
  container: 'map',
  style: 'mapbox://styles/mapbox/light-v{{constants.VERSION_LIGHT_STYLE}}',
  center: [-96, 37.8],
  zoom: 3
});

// code from the next step will go here!

</script>

</body>
</html>
```

As you can see above, the Mapbox GL JS map requires several options:

- `container`: the `id` of the `<div>` element on the page where the map should live. In this case, the `id` for the `<div>` is `'map'`.
- `style`: the style URL for the map style. In this case, use the Mapbox Light map which has the style URL `mapbox://styles/mapbox/light-{{constants.VERSION_LIGHT_STYLE}}`.
- `center`: the initial centerpoint of the map in `[longitude, latitude]` format.
- `zoom`: the initial zoom level of the map.


### Load GeoJSON data

Load your data by adding inline GeoJSON to your HTML file. This GeoJSON will be used to determine where your markers will appear on the map.

Copy and paste the following after the code that initializes your map but before the `</script>` tag. This code declares a variable `geojson` that is set equal to GeoJSON data.

```js
var geojson = {
  type: 'FeatureCollection',
  features: [{
    type: 'Feature',
    geometry: {
      type: 'Point',
      coordinates: [-77.032, 38.913]
    },
    properties: {
      title: 'Mapbox',
      description: 'Washington, D.C.'
    }
  },
  {
    type: 'Feature',
    geometry: {
      type: 'Point',
      coordinates: [-122.414, 37.776]
    },
    properties: {
      title: 'Mapbox',
      description: 'San Francisco, California'
    }
  }]
};
```

{{
  <Note imageComponent={<BookImage />}>
    <p>If you have a large GeoJSON file, you may want to load it as an external source rather than adding it inline. You can do so by linking to its URL, if it's hosted remotely, or by using an AJAX call to load locally or from a third-party API.</p>
  </Note>
}}

## Add HTML markers

Now that you've loaded your data, add code to create an HTML DOM element for each marker and bind it to the GeoJSON features using the Mapbox GL JS [Marker](https://www.mapbox.com/mapbox-gl-js/api/#marker) method. You'll be using the image you downloaded at the beginning of this tutorial, which should be saved in your project folder.

When you add a marker using the Marker method, you are attaching an empty `div` to each point in your GeoJSON. You'll need to specify the style of the marker before adding it to the map.

### Style markers

First, add the CSS you'll need to style your markers. In this case, add the image file you downloaded as the `background-image` for a class called `marker`. In your same `index.html` file, copy and paste the code inside your `style` tag below the `#map` declaration.

```css
.marker {
  background-image: url('mapbox-icon.png');
  background-size: cover;
  width: 50px;
  height: 50px;
  border-radius: 50%;
  cursor: pointer;
}
```

### Add markers to the map

Next, add the JavaScript needed to create the markers and add them to the map. Copy and paste the following code within your `script` tag after the end of your `map` object declaration but before the closing script tag.

```js
// add markers to map
geojson.features.forEach(function(marker) {

  // create a HTML element for each feature
  var el = document.createElement('div');
  el.className = 'marker';

  // make a marker for each feature and add to the map
  new mapboxgl.Marker(el)
    .setLngLat(marker.geometry.coordinates)
    .addTo(map);
});
```

Save the file and refresh your browser. You should see you map displaying with your custom HTML markers.


## Add popups

As your final step, add popups to your markers using Mapbox GL JS. You'll do this within the `mapboxgl.Marker` declaration.

### Style popups

First, add the CSS code you'll need to style your popups. In the same `index.html` file, copy and paste the code inside your `style` tag below the `.marker` declaration.

```css
.mapboxgl-popup {
  max-width: 200px;
}

.mapboxgl-popup-content {
  text-align: center;
  font-family: 'Open Sans', sans-serif;
}
```

### Attach popups to markers

Next, you'll add the JavaScript needed to add popups containing information about each point and display the popup when a marker is clicked:

1. Copy and paste the `.setPopup` code below after the `.setLngLat()` method and before the `.addTo()` method within your `script` tags.
  - Make sure you're using the correct key for the data you want to display in your popups. In this example, you will be displaying your data's `title` and `description` properties.
1. Save your file and refresh your browser.
1. You should be able to click on the markers and see popups displayed.


```js
new mapboxgl.Marker(el)
  .setLngLat(marker.geometry.coordinates)
  .setPopup(new mapboxgl.Popup({ offset: 25 }) // add popups
    .setHTML('<h3>' + marker.properties.title + '</h3><p>' + marker.properties.description + '</p>'))
  .addTo(map);
```

Notice that you've added an offset value when you declare popups using the [`mapboxgl.Popup`](https://www.mapbox.com/mapbox-gl-js/api/#popup) method to make sure your popups are centered over your markers.


## Final product

You've made an interactive marker map with custom data and styling using Mapbox GL JS.

{{
  <DemoIframe src="/help/demos/custom-markers-gl-js/index.html" />
}}

## Next steps

Now that you've created a project using Mapbox GL JS, we recommend checking out our other tutorials to extend your web app:

- [Add points to a map](/help/tutorials/add-points-pt-1/) using Mapbox Studio and Mapbox GL JS.
- [Build a store locator](/help/tutorials/building-a-store-locator/) using Mapbox GL JS.
- [Show changes over time](/help/tutorials/show-changes-over-time/) with Mapbox GL JS.
- [Analyze data with Turf.js](/help/tutorials/analysis-with-turf/) and Mapbox GL JS.

Explore our [Mapbox GL JS examples](https://www.mapbox.com/mapbox-gl-js/examples/) for more ideas on how to extend your project and code to get you started.
