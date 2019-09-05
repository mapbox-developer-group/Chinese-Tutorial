---
title: Build a store locator using Mapbox.js
description: Build a map application with Mapbox.js. This guide walks you through all the code that you need to build a store locator.
thumbnail: buildingAStoreLocatorJs
level: 3
topics:
- web apps
language:
- JavaScript
prereq: Familiarity with front-end development concepts. Some advanced JavaScript required.
legacy: true
prependJs:
  - "import * as constants from '../../constants';"
  - "import Icon from '@mapbox/mr-ui/icon';"
  - "import { LegacyNote } from '../../components/legacy-note';"
  - "import { sweetgreenLocations } from '../../snippets/sweetgreen-locations';"
  - "import UserAccessToken from '../../components/user-access-token';"
  - "import DemoIframe from '@mapbox/dr-ui/demo-iframe';"
  - "import Button from '@mapbox/mr-ui/button';"
contentType: tutorial
---

{{
  <LegacyNote
    legacyProduct='Mapbox.js'
    alternativeResource={{
      title: 'Build a store locator with Mapbox GL JS',
      link: '/help/tutorials/building-a-store-locator/'
    }}
  />
}}

In this tutorial, you'll learn how to create a store locator map. Using your new map, you'll be able to browse through a list of locations from a sidebar and select a specific store to view more information. Selecting a [marker](/help/glossary/marker/) on the map will highlight the selected store on the sidebar.

{{
  <DemoIframe gl={false} src="/help/demos/store-locator/step-four.html" />
}}

For this tutorial, you're going to use [Sweetgreen](http://sweetgreen.com), a local salad shop, as an example. They have a healthy number of locations, plus their salads are delicious.

This guide gets into a few more advanced JavaScript concepts with [Mapbox.js](https://www.mapbox.com/mapbox.js/). If you're new to Mapbox.js, we recommend you read our [Extending with Mapbox.js guide](/help/tutorials/extending-interactivity/) first.

## Getting started

Before writing any code, create a local folder called "store-locator" to house your project files. This folder is referred to as your *project folder* from here on out.

There are a few resources you'll need to gather before we get started:

- [**A tileset ID**](/help/glossary/tileset-id). A tileset ID points to a unique map you have created with Mapbox. For the purposes of this guide, you'll use the tileset ID `mapbox.k8xv42t9`, but you can substitute your own custom tileset if you like!
- [**Your access token**](/help/glossary/access-token/). The token is used to associate a map with your account:

```js
L.mapbox.accessToken = '{{ <UserAccessToken /> }}';
```

- [__Mapbox.js__](https://www.mapbox.com/mapbox.js/). The Mapbox JavaScript API for building maps.

- __Data__. We collected Sweetgreen's locations and marked up the data in GeoJSON for your convenience.

- __Custom map marker__. Your finished map will have some fancy custom images for its markers. [Save the image](/help/demos/store-locator/marker.png) to your project folder.

- __A text editor.__ You'll be writing HTML, CSS, and JavaScript after all.

<h2 id='add-structure'>Add structure</h2>

In your project folder, create an `index.html` file. Set up the document by adding reference the Mapbox.js JavaScript library and its accompanying CSS:

```html
<script src='https://api.mapbox.com/mapbox.js/{{constants.VERSION_MAPBOXJS}}/mapbox.js'></script>
<link href='https://api.mapbox.com/mapbox.js/{{constants.VERSION_MAPBOXJS}}/mapbox.css' rel='stylesheet' />
```

Next, markup the page to create a map container and sidebar listing:

```html
<div class='sidebar pad2'>Listing</div>
<div id='map' class='map pad2'>Map</div>
```

Apply a bit of CSS so you can visualize what the layout looks like:

```css
body {
  background: #404040;
  color: #f8f8f8;
  font: 500 20px/26px 'Helvetica Neue', Helvetica, Arial, Sans-serif;
  margin: 0;
  padding: 0;
  -webkit-font-smoothing: antialiased;
}

/**
 * The page is split between map and sidebar - the sidebar gets 1/3, map
 * gets 2/3 of the page. You can adjust this to your personal liking.
 */
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
  <DemoIframe gl={false} src="/help/demos/store-locator/step-one.html" />
}}

## Initialize map

Now that you have set up the structure of the project, bring your map to life by initializing it with Mapbox.js.

First, create an instance of `L.mapbox.map` and store it in a variable called `map`. You'll also use `setView` to focus the map to Washington DC where all the shops are located. Here, you'll need to update your tileset ID and access token. Add the script under your HTML:

```js
L.mapbox.accessToken = '{{ <UserAccessToken /> }}';
var map = L.mapbox.map('map')
    .setView([38.909671288923, -77.034084142948], 13)
    .addLayer(L.mapbox.styleLayer('mapbox://styles/mapbox/light-v10'));
```

## Load data

Before you put any markers on your map, store all the GeoJSON data you downloaded above in a variable called `geojson`. Once the map is initialized, you can use `featureLayer.setGeoJSON` to load features on the map by referencing the `geojson` variable:

```js
L.mapbox.accessToken = '{{ <UserAccessToken /> }}';
var geojson = {{sweetgreenLocations}};
var map = L.mapbox.map('map')
  .setView([38.909671288923, -77.034084142948], 13)
  .addLayer(L.mapbox.styleLayer('mapbox://styles/mapbox/light-v10'))
  .featureLayer.setGeoJSON(geojson);
```

{{
  <DemoIframe gl={false} src="/help/demos/store-locator/step-two.html" />
}}

Alternatively, you can save the GeoJSON as a `.geojson` file and [load the file on to the map](https://www.mapbox.com/mapbox.js/example/v1.0.0/geojson-marker-from-url/). If you do this, you will need to run your application from a local web server (something like `http://localhost/store-locator.html`). If you try to open your `index.html` file directly in your browser, you will receive a [Cross-origin Resource Sharing](http://en.wikipedia.org/wiki/Cross-origin_resource_sharing) (CORS) error.

## Build listings and tooltips

You have some markers on the map, but you still need to build the listings and tooltips. Rather than creating each manually, you can put JavaScript to work to read through the GeoJSON and dynamically build listings and set tooltips for us. This means that if you need to add a location then you *only* need to update the GeoJSON.

`L.mapbox.featureLayer` allows you to iterate over data before it is added to the map using the `eachLayer` method. This means that JavaScript will run through each point, populate the custom tooltip, add each location listing to the sidebar, and listen for and respond to a user's click event to track when a marker or listing is selected:

```js
var locations = L.mapbox.featureLayer().addTo(map);
locations.setGeoJSON(geojson);
locations.eachLayer(function(locale) {
  // Iterate over each marker.
});
```

The variable `locations` references your new `L.mapbox.featureLayer`, then taps into `eachLayer`. The passed parameter `locale` is each marker object.

At this point you can start populating content into each listing using information provided by each `locale`. Nice! But you still need to update the sidebar HTML to hold the listing information:

```html
<div class='sidebar'>
  <div class='heading'>
    <h1>Our locations</h1>
  </div>
  <div id='listings' class='listings'></div>
</div>
```

Next, update your CSS to accommodate your layout changes:

```css
body {
  color: #404040;
  font: 400 15px/22px 'Helvetica Neue', Sans-serif;
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

.quiet {
  color: #888;
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

.listings .item:last-child {
  border-bottom: none;
}

.listings .item .title {
  display: block;
  color: #00853e;
  font-weight: 700;
}

.listings .item .title small {
  font-weight: 400;
}

.listings .item.active .title,
.listings .item .title:hover {
  color: #8cc63f;
}

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

.clearfix {
  display: block;
}

.clearfix::after {
  content: '.';
  display: block;
  height: 0;
  clear: both;
  visibility: hidden;
}

/* Marker tweaks */
.leaflet-popup-close-button {
  display: none;
}

.leaflet-popup-content {
  font: 400 15px/22px 'Source Sans Pro', 'Helvetica Neue', Sans-serif;
  padding: 0;
  width: 200px;
}

.leaflet-popup-content-wrapper {
  padding: 0;
}

.leaflet-popup-content h3 {
  background: #91c949;
  color: #fff;
  margin: 0;
  display: block;
  padding: 10px;
  border-radius: 3px 3px 0 0;
  font-weight: 700;
  margin-top: -15px;
}

.leaflet-popup-content div {
  padding: 10px;
}

.leaflet-container .leaflet-marker-icon {
  cursor: pointer;
}
```

Now you can put the finishing touches on your script. Outside of `eachLayer`, create a variable called `listings` that selects the listing container in the HTML. With this selected you can append each listing into the sidebar:

```js
var listings = document.getElementById('listings');

locations.eachLayer(function(locale) {
  // Shorten locale.feature.properties to `prop` so we're not
  // writing this long form over and over again.
  var prop = locale.feature.properties;

  var listing = listings.appendChild(document.createElement('div'));
  listing.className = 'item';

  var link = listing.appendChild(document.createElement('a'));
  link.href = '#';
  link.className = 'title';
  link.innerHTML = prop.address;

  if (prop.crossStreet) {
    link.innerHTML += ' <br /><small>' + prop.crossStreet + '</small>';
  }

  var details = listing.appendChild(document.createElement('div'));
  details.innerHTML = prop.city;

  if (prop.phone) {
    details.innerHTML += ' &middot; ' + prop.phoneFormatted;
  }
});
```

The `link` variable should have the special behavior of panning to its associated marker on the map. By binding an `onclick` event, you can target the current `locale` object in context, pan the map to the object's coordinates, and trigger its tooltip to appear.

```js
link.onclick = function() {
  // 1. Toggle an active class for `listing`. View the source in the demo link for example.
  // 2. When a menu item is clicked, animate the map to center
  // its associated locale and open its popup.
  map.setView(locale.getLatLng(), 16);
  locale.openPopup();
};
```

Each marker tooltip requires unique information. Use the `bindPopup` method to pass content to your popups.

```js
var popup = 'Sweetgreen';
locale.bindPopup(popup);
```

Finally, make sure that when a user clicks a marker that it sets the associated listing in the sidebar as active by binding a `click` event handler to each `locale`.

```js
locale.on('click', function() {
  // 1. Toggle an active class for `listing`. View the source in the demo link for example.

  // 2. center the map on the selected marker.
  map.setView(locale.getLatLng(), 16);
});
```

At this point, your whole script should look like:

```js
var listings = document.getElementById('listings');
var locations = L.mapbox.featureLayer().addTo(map);

locations.setGeoJSON(geojson);

function setActive(el) {
  var siblings = listings.getElementsByTagName('div');
  for (var i = 0; i < siblings.length; i++) {
    siblings[i].className = siblings[i].className
      .replace(/active/, '').replace(/\s\s*$/, '');
  }

  el.className += ' active';
}

locations.eachLayer(function(locale) {

  // Shorten locale.feature.properties to `prop` so you don't
  // have to write this long form over and over again.
  var prop = locale.feature.properties;

  // Each marker on the map.
  var popup = '<h3>Sweetgreen</h3><div>' + prop.address;

  var listing = listings.appendChild(document.createElement('div'));
  listing.className = 'item';

  var link = listing.appendChild(document.createElement('a'));
  link.href = '#';
  link.className = 'title';

  link.innerHTML = prop.address;
  if (prop.crossStreet) {
    link.innerHTML += '<br /><small class="quiet">' + prop.crossStreet + '</small>';
    popup += '<br /><small class="quiet">' + prop.crossStreet + '</small>';
  }

  var details = listing.appendChild(document.createElement('div'));
  details.innerHTML = prop.city;
  if (prop.phone) {
    details.innerHTML += ' &middot; ' + prop.phoneFormatted;
  }

  link.onclick = function() {
    setActive(listing);

    // When a menu item is clicked, animate the map to center
    // its associated locale and open its popup.
    map.setView(locale.getLatLng(), 16);
    locale.openPopup();
    return false;
  };

  // Marker interaction
  locale.on('click', function(e) {
    // 1. center the map on the selected marker.
    map.panTo(locale.getLatLng());

    // 2. Set active the markers associated listing.
    setActive(listing);
  });

  popup += '</div>';
  locale.bindPopup(popup);
});
```

{{
  <DemoIframe gl={false} src="/help/demos/store-locator/step-three.html" />
}}

There's a lot of code inside the `eachLayer` function because it makes sure each event is bound to its respective elements.

## Add custom markers

You *could* add style to our markers by adding property keys to each feature in the GeoJSON, but for this example you want to give your stores unique and fancy markers.

To give your markers a custom icon, use the `setIcon` function inside the `locations.eachLayer` function you created earlier. In `setIcon`, pass [`L.icon`](https://www.mapbox.com/mapbox.js/api/{{constants.VERSION_MAPBOXJS}}/l-icon/) with your own custom options by copying and pasting the following right after `locale.bindPopup(popup);`:

```js
locale.setIcon(L.icon({
  iconUrl: 'marker.png',
  iconSize: [56, 56],
  iconAnchor: [28, 28],
  popupAnchor: [0, -34]
}));
```

Freshen up your map's type with the Source Sans Pro font:

```html
<link href='https://fonts.googleapis.com/css?family=Source+Sans+Pro:400,700' rel='stylesheet'>
```

You'll also need to update the `font` property in `body` style:

```css
font:400 15px/22px 'Source Sans Pro', 'Helvetica Neue', Sans-serif;
```

## Finished product

You have completed the store locator!

{{
  <DemoIframe gl={false} src="/help/demos/store-locator/step-four.html" />
}}

{{
<Button href="/help/demos/store-locator/store-locator-final.zip" passthroughProps={{ download: "store-locator-final" }} >
    <Icon name='arrow-down' inline={true} /> Download the completed project
</Button>
}}

If you're interested in loading your GeoJSON from a file, [here's the slightly modified code](/help/demos/store-locator/store-locator-final-alt.zip). Heads up! You'll need to serve these files to avoid a CORS error.

## Next steps

Nice job! We hope you're set with the tools to create your own store locator.

For bonus points, if a store's location data is added to [Foursquare](https://foursquare.com) you could extend this example even further by pulling data directly from [Foursquare's API](https://developer.foursquare.com/docs/). API requests return geolocated information and details about a place. This would allow for more dynamic data like user submitted images or the total number of check-ins a location has received.
