---
title: Build a store locator using Mapbox GL JS
description: Build a map application with Mapbox GL JS. This guide walks you through all the code that you need to build a store locator.
thumbnail: buildingAStoreLocator
level: 3
topics:
- web apps
language:
- JavaScript
prereq: Familiarity with front-end development concepts. Some advanced JavaScript required.
prependJs:
  - "import * as constants from '../../constants';"
  - "import Icon from '@mapbox/mr-ui/icon';"
  - "import { sweetgreenLocations } from '../../snippets/sweetgreen-locations';"
  - "import UserAccessToken from '../../components/user-access-token';"
  - "import DemoIframe from '@mapbox/dr-ui/demo-iframe';"
  - "import { DemoLink } from '../../components/demo-link';"
  - "import Button from '@mapbox/mr-ui/button';"
contentType: tutorial
---

This guide will walk you through how to create a store locator map using Mapbox GL JS. You'll be able to browse all the locations from a sidebar and select a specific store to view more information. Selecting a [marker](/help/glossary/marker/) on the map will highlight the selected store on the sidebar.

{{
  <DemoIframe src="/help/demos/gl-store-locator/step-five.html" />
}}

You will use [Sweetgreen](http://sweetgreen.com), a local salad shop, as an example. They have a healthy number of locations, plus their salads are delicious!

This guide shows you how to use [Mapbox GL JS](https://www.mapbox.com/mapbox-gl-js/) to build an interactive web map. If you're new to Mapbox GL JS, you might want to read our guide on Mapbox [web applications](/help/how-mapbox-works/web-apps/) first.

## Getting started

For this project, we recommend that you create a local folder called "store-locator" to house your project files. You'll see this folder referred to as your *project folder*.

There are a few resources you'll need before getting started:

- [__A style URL__](/help/glossary/style-url). A style URL points to a unique map you have created with Mapbox Studio. You can either create a custom style with the [Mapbox Studio style editor](https://www.mapbox.com/studio-manual/reference/styles/) or use a [Mapbox style](https://www.mapbox.com/studio/styles).

- [__An access token__](/help/glossary/access-token/) from your account. You will use an access token to associate a map with your account. Your access token is on the  [Account page](https://www.mapbox.com/account/).

- [__Mapbox GL JS__](https://www.mapbox.com/mapbox-gl-js/). The Mapbox JavaScript library that uses WebGL to render interactive maps from Mapbox GL styles.

- __A text editor.__ You'll be writing HTML, CSS, and JavaScript after all.

- __Data__. We collected some of Sweetgreen's locations and marked up the data in GeoJSON.

- __Custom map marker__. You'll be using an image for your map marker. Save the image to your project folder.

{{
<Button href="/help/demos/store-locator/marker.png" passthroughProps={{ download: "marker" }} >
    <Icon name='arrow-down' inline={true} /> Download custom marker
</Button>
}}

## Add structure

In your project folder, create an `index.html` file. Set up the document by adding Mapbox GL JS and CSS to your `head`:

```html
<script src='https://api.tiles.mapbox.com/mapbox-gl-js/{{constants.VERSION_MAPBOXGLJS}}/mapbox-gl.js'></script>
<link href='https://api.tiles.mapbox.com/mapbox-gl-js/{{constants.VERSION_MAPBOXGLJS}}/mapbox-gl.css' rel='stylesheet' />
```

Next, markup the page to create a map container and sidebar listing:

```html
<div class='sidebar pad2'>Listing</div>
<div id='map' class='map pad2'>Map</div>
```

Then, apply some CSS to create the page layout:

```css
body {
  background: #404040;
  color: #f8f8f8;
  font: 500 20px/26px 'Helvetica Neue', Helvetica, Arial, Sans-serif;
  margin: 0;
  padding: 0;
  -webkit-font-smoothing: antialiased;
}

/* The page is split between map and sidebar - the sidebar gets 1/3, map
gets 2/3 of the page. You can adjust this to your personal liking. */
.sidebar {
  width: 33.3333%;
}

.map {
  border-left: 1px solid #fff;
  position: absolute;
  left: 33.3333%;
  width: 66.6666%;
  top: 0;
  bottom: 0;
}

.pad2 {
  padding: 20px;
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
}
```

{{
  <DemoIframe src="/help/demos/gl-store-locator/step-one.html" />
}}

## Initialize the map

Now that you have the structure of the page, initialize the map with Mapbox GL JS.

First, add your access token using `mapboxgl.accessToken`. Then, create a new `map` object using `new mapboxgl.Map()` and store it in a variable called `map`:

```js
mapboxgl.accessToken = '{{ <UserAccessToken /> }}';
// This adds the map to your page
var map = new mapboxgl.Map({
  // container id specified in the HTML
  container: 'map',
  // style URL
  style: 'mapbox://styles/mapbox/light-v{{constants.VERSION_LIGHT_STYLE}}',
  // initial position in [lon, lat] format
  center: [-77.034084, 38.909671],
  // initial zoom
  zoom: 14
});
```

As you can see above, the Mapbox GL JS map requires several options:

- `container`: the `id` of the `<div>` element on the page where the map should live. In this case, the `id` for the `<div>` is `'map'`.

- `style`: the [style URL](/help/glossary/style-url/) for the map style. In this case, use the {{ <DemoLink href="https://api.mapbox.com/styles/v1/mapbox/light-v{constants.VERSION_LIGHT_STYLE}.html?title=true&access_token=MapboxAccessToken#1.07/0.0/0.0" text="Mapbox Light map" /> }} which has the style URL `mapbox://styles/mapbox/light-{{constants.VERSION_LIGHT_STYLE}}`.

- `center`: the initial centerpoint of the map in [longitude, latitude] format.

- `zoom`: the initial zoom level of the map.

## Load data

With Mapbox GL JS, map rendering happens in the browser. For the browser to render your map, you need to add a layer with geospatial data and instructions for how that data should be rendered.

To add a source to the map, your code needs to access the geospatial data. Store all the GeoJSON data in `sweetgreen.geojson` in a variable called `stores`:

```js
var stores = {{ sweetgreenLocations }};
```

Now you can add a layer that contains this data and describes how it should be rendered. Add the data to your map once the map loads using `addLayer()`. Create a new layer, and specify `stores` as a GeoJSON data source. Then, add instructions for rendering the source. This example only adds minimal styling --- for full details on all the layer styling options, see the [Mapbox Style Specification](https://www.mapbox.com/mapbox-gl-style-spec/):

```js
map.on('load', function(e) {
  // Add the data to your map as a layer
  map.addLayer({
    id: 'locations',
    type: 'symbol',
    // Add a GeoJSON source containing place coordinates and information.
    source: {
      type: 'geojson',
      data: stores
    },
    layout: {
      'icon-image': 'restaurant-15',
      'icon-allow-overlap': true,
    }
  });
});
```

_Note: `restaurant-15` refers to an icon in the Mapbox Light style you added earlier in the code._

{{
  <DemoIframe src="/help/demos/gl-store-locator/step-two.html" />
}}

## Build store listing

Now that the points are on your map, it's time to build the restaurant location listing by iterating through the GeoJSON and creating a list of restaurants dynamically. This means that if you need to add a location then you *only* need to update the GeoJSON.

First, update the sidebar HTML to hold the listing information and update your CSS to accommodate the layout changes:

```html
<div class='sidebar'>
  <div class='heading'>
    <h1>Our locations</h1>
  </div>
  <div id='listings' class='listings'></div>
</div>
```

```css
body {
  color: #404040;
  font: 400 15px/22px 'Source Sans Pro', 'Helvetica Neue', Sans-serif;
  margin: 0;
  padding: 0;
  -webkit-font-smoothing: antialiased;
}

* {
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
}

h1 {
  font-size: 22px;
  margin: 0;
  font-weight: 400;
  line-height: 20px;
  padding: 20px 2px;
}

a {
  color: #404040;
  text-decoration: none;
}

a:hover {
  color: #101010;
}

.sidebar {
  position: absolute;
  width: 33.3333%;
  height: 100%;
  top: 0;
  left: 0;
  overflow: hidden;
  border-right: 1px solid rgba(0, 0, 0, 0.25);
}

.pad2 {
  padding: 20px;
}

.map {
  position: absolute;
  left: 33.3333%;
  width: 66.6666%;
  top: 0;
  bottom: 0;
}

.heading {
  background: #fff;
  border-bottom: 1px solid #eee;
  height: 60px;
  line-height: 60px;
  padding: 0 10px;
}

.listings {
  height: 100%;
  overflow: auto;
  padding-bottom: 60px;
}

.listings .item {
  display: block;
  border-bottom: 1px solid #eee;
  padding: 10px;
  text-decoration: none;
}

.listings .item:last-child { border-bottom: none; }

.listings .item .title {
  display: block;
  color: #00853e;
  font-weight: 700;
}

.listings .item .title small { font-weight: 400; }

.listings .item.active .title,
.listings .item .title:hover { color: #8cc63f; }

.listings .item.active {
  background-color: #f8f8f8;
}

::-webkit-scrollbar {
  width: 3px;
  height: 3px;
  border-left: 0;
  background: rgba(0, 0, 0, 0.1);
}

::-webkit-scrollbar-track {
  background: none;
}

::-webkit-scrollbar-thumb {
  background: #00853e;
  border-radius: 0;
}

.clearfix { display: block; }

.clearfix::after {
  content: '.';
  display: block;
  height: 0;
  clear: both;
  visibility: hidden;
}
```

Next, build a function to iterate through the Sweetgreen locations and add each one to the sidebar listing:

```js
function buildLocationList(data) {
  // Iterate through the list of stores
  for (i = 0; i < data.features.length; i++) {
    var currentFeature = data.features[i];
    // Shorten data.feature.properties to `prop` so we're not
    // writing this long form over and over again.
    var prop = currentFeature.properties;
    // Select the listing container in the HTML and append a div
    // with the class 'item' for each store
    var listings = document.getElementById('listings');
    var listing = listings.appendChild(document.createElement('div'));
    listing.className = 'item';
    listing.id = 'listing-' + i;

    // Create a new link with the class 'title' for each store
    // and fill it with the store address
    var link = listing.appendChild(document.createElement('a'));
    link.href = '#';
    link.className = 'title';
    link.dataPosition = i;
    link.innerHTML = prop.address;

    // Create a new div with the class 'details' for each store
    // and fill it with the city and phone number
    var details = listing.appendChild(document.createElement('div'));
    details.innerHTML = prop.city;
    if (prop.phone) {
      details.innerHTML += ' &middot; ' + prop.phoneFormatted;
    }
  }
}
```

Then, you will need to call this function when the map loads. You can do this by adding `buildLocationList(stores);` inside your `map.on('load', ...)` function after `addLayer()`. The result will look like this:

{{
  <DemoIframe src="/help/demos/gl-store-locator/step-three.html" />
}}

## Make the map interactive

When a user clicks a link in the sidebar or on a point on the map, you want three things to happen:

1. The map to fly to the associated store location.
2. A popup to be displayed at that point.
3. The listing to be highlighted in the sidebar.

This will require a bit more code, but you can do it!

### Define interactivity functions

First, define two functions: one that flies the map to the correct store, and one that displays a popup at that point. These functions will be fired both when a user clicks on a link in the sidebar listing and when a user clicks on a store location in the map. (Highlighting the listing on the sidebar will be handled separately for the two different click events.)

```js
function flyToStore(currentFeature) {
  map.flyTo({
    center: currentFeature.geometry.coordinates,
    zoom: 15
  });
}

function createPopUp(currentFeature) {
  var popUps = document.getElementsByClassName('mapboxgl-popup');
  // Check if there is already a popup on the map and if so, remove it
  if (popUps[0]) popUps[0].remove();

  var popup = new mapboxgl.Popup({ closeOnClick: false })
    .setLngLat(currentFeature.geometry.coordinates)
    .setHTML('<h3>Sweetgreen</h3>' +
      '<h4>' + currentFeature.properties.address + '</h4>')
    .addTo(map);
}
```

You can also style your popups using CSS:

```css
/* Marker tweaks */
.mapboxgl-popup-close-button {
  display: none;
}

.mapboxgl-popup-content {
  font: 400 15px/22px 'Source Sans Pro', 'Helvetica Neue', Sans-serif;
  padding: 0;
  width: 180px;
}

.mapboxgl-popup-content-wrapper {
  padding: 1%;
}

.mapboxgl-popup-content h3 {
  background: #91c949;
  color: #fff;
  margin: 0;
  display: block;
  padding: 10px;
  border-radius: 3px 3px 0 0;
  font-weight: 700;
  margin-top: -15px;
}

.mapboxgl-popup-content h4 {
  margin: 0;
  display: block;
  padding: 10px;
  font-weight: 400;
}

.mapboxgl-popup-content div {
  padding: 10px;
}

.mapboxgl-container .leaflet-marker-icon {
  cursor: pointer;
}

.mapboxgl-popup-anchor-top > .mapboxgl-popup-content {
  margin-top: 15px;
}

.mapboxgl-popup-anchor-top > .mapboxgl-popup-tip {
  border-bottom-color: #91c949;
}
```

For the `.remove()` method to work in older browsers, you will need to include the code below at the beginning of your script:

```js
// This will let you use the .remove() function later on
if (!('remove' in Element.prototype)) {
  Element.prototype.remove = function() {
    if (this.parentNode) {
      this.parentNode.removeChild(this);
    }
  };
}
```

See the [HTML documentation](https://developer.mozilla.org/en-US/docs/Web/API/ChildNode/remove) for more information.

### Add event listeners

Now that you've defined these two functions, you want them to fire when a user clicks on a restaurant in the sidebar listing or when a user clicks on a restaurant on the map. To do this, you will add _event listeners_ that listen for "click" events and execute some function when they happen. You will add two event listeners: one for when a link in the sidebar is clicked and one for when a location on the map is clicked.

Use this code for when a link is clicked:

```js
// Add an event listener for the links in the sidebar listing
link.addEventListener('click', function(e) {
  // Update the currentFeature to the store associated with the clicked link
  var clickedListing = data.features[this.dataPosition];
  // 1. Fly to the point associated with the clicked link
  flyToStore(clickedListing);
  // 2. Close all other popups and display popup for clicked store
  createPopUp(clickedListing);
  // 3. Highlight listing in sidebar (and remove highlight for all other listings)
  var activeItem = document.getElementsByClassName('active');
  if (activeItem[0]) {
    activeItem[0].classList.remove('active');
  }
  this.parentNode.classList.add('active');
});
```

Use this code for when a location on the map is clicked:

```js
// Add an event listener for when a user clicks on the map
map.on('click', function(e) {
  // Query all the rendered points in the view
  var features = map.queryRenderedFeatures(e.point, { layers: ['locations'] });
  if (features.length) {
    var clickedPoint = features[0];
    // 1. Fly to the point
    flyToStore(clickedPoint);
    // 2. Close all other popups and display popup for clicked store
    createPopUp(clickedPoint);
    // 3. Highlight listing in sidebar (and remove highlight for all other listings)
    var activeItem = document.getElementsByClassName('active');
    if (activeItem[0]) {
      activeItem[0].classList.remove('active');
    }
    // Find the index of the store.features that corresponds to the clickedPoint that fired the event listener
    var selectedFeature = clickedPoint.properties.address;

    for (var i = 0; i < stores.features.length; i++) {
      if (stores.features[i].properties.address === selectedFeature) {
        selectedFeatureIndex = i;
      }
    }
    // Select the correct list item using the found index and add the active class
    var listing = document.getElementById('listing-' + selectedFeatureIndex);
    listing.classList.add('active');
  }
});
```

{{
  <DemoIframe src="/help/demos/gl-store-locator/step-four.html" />
}}

## Add custom markers

This section will walk you through how to replace the existing standard symbol layer with custom markers. First, you will need to remove the existing symbol layer and related functions. Remove the symbol layer by deleting the `.addLayer()` function from your code, and replace it with the `.addSource()` code below. Instead of styling the symbol layer with `addLayer`, you will use the Markers API to add an image to each point in the GeoJSON data:

```js
map.addSource('places', {
  type: 'geojson',
  data: stores
});
```


You'll also want to delete the [function that listened for a click on a symbol](#symbol-click) to fly to the location, display a popup, and highlight the list item. Then, add the custom Sweetgreen icons to the map using `mapboxgl.Marker()` objects. Unlike the symbol layer, which has symbols embedded in the map, `mapboxgl.Marker()` objects are HTML DOM elements that can be styled with CSS. Add a new class to the CSS called `.marker` and set the Sweetgreen marker you [downloaded](/help/demos/store-locator/marker.png) earlier as the `background-image`:

```css
.marker {
  border: none;
  cursor: pointer;
  height: 56px;
  width: 56px;
  background-image: url(marker.png);
  background-color: rgba(0, 0, 0, 0);
}
```

To add the new markers to the map, iterate through all stores and add the new marker to the map at each location:

```js
stores.features.forEach(function(marker) {
  // Create a div element for the marker
  var el = document.createElement('div');
  // Add a class called 'marker' to each div
  el.className = 'marker';
  // By default the image for your custom marker will be anchored
  // by its center. Adjust the position accordingly
  // Create the custom markers, set their position, and add to map
  new mapboxgl.Marker(el, { offset: [0, -23] })
    .setLngLat(marker.geometry.coordinates)
    .addTo(map);
});
```

### Add new event listeners

Now that you have replaced your symbols with markers, you will need to re-add some code for flying to the position on the map, displaying a popup, and highlighting the `list` item in the sidebar when clicking on the marker. Within your `forEach` function from above, add an event listener:

```js
el.addEventListener('click', function(e) {
  var activeItem = document.getElementsByClassName('active');
  // 1. Fly to the point
  flyToStore(marker);
  // 2. Close all other popups and display popup for clicked store
  createPopUp(marker);
  // 3. Highlight listing in sidebar (and remove highlight for all other listings)
  e.stopPropagation();
  if (activeItem[0]) {
    activeItem[0].classList.remove('active');
  }
  var listing = document.getElementById('listing-' + i);
  console.log(listing);
  listing.classList.add('active');
});
```

### Final tweaks

You will need to adjust the position of the popup to account for the added height of the marker. You can do this using CSS:

```css
.mapboxgl-popup {
  padding-bottom: 50px;
}
```

At this point, you can also freshen up the type with Source Sans Pro:

```html
<link href='https://fonts.googleapis.com/css?family=Source+Sans+Pro:400,700' rel='stylesheet'>
```

You'll need to update the `font` property in `body` style:

```css
font: 400 15px/22px 'Source Sans Pro', 'Helvetica Neue', Sans-serif;
```

## Finished product

You have completed the store locator.

{{
  <DemoIframe src="/help/demos/gl-store-locator/step-five.html" />
}}

## Next steps

After following this guide, you have the tools you need to create your own store locator. Explore more Mapbox GL JS resources on our [help page](/help/tutorials/).
