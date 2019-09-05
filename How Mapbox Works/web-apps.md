---
title: Web applications
description: Learn how Mapbox’s JavaScript libraries work and how to integrate them into your web applications.
image: /img/narrative/web-develop.svg
topics:
  - web apps
prependJs:
  - "import * as constants from '../../constants';"
  - "import Note from '@mapbox/dr-ui/note';"
  - "import BookImage from '@mapbox/dr-ui/book-image';"
  - "import DemoIframe from '@mapbox/dr-ui/demo-iframe';"
  - "import { LegacyNote } from '../../components/legacy-note';"
contentType: guide
---

Mapbox provides many tools to build maps into your website or web-based application. [Mapbox GL JS](https://www.mapbox.com/mapbox-gl-js) and [Mapbox.js](https://www.mapbox.com/mapbox.js) are both open source JavaScript libraries you can use to display your Mapbox maps, add interactivity, and customize the map experience in your application. We also provide many plugins for extending your web map's functionality with drawing tools and interfaces to Mapbox web services APIs like the Mapbox Geocoding API or Mapbox Directions API. Building webpages or web applications with our JavaScript libraries will require writing code, but this guide is designed to provide you with the resources to get started.

<div class='bg-white border-b'>
  <div class='txt-m txt-bold'>Web app using Mapbox GL JS</div>
  <div class='txt-xs pb6'>Combine our JavaScript library with HTML, CSS, and JavaScript</div>
</div>

{{
  <DemoIframe src="/help/demos/gl-store-locator/step-five.html" />
}}

{{<div className='caption'>}}
This web application uses a combination of HTML, CSS, JavaScript, and  **Mapbox GL JS**, our GL-based JavaScript library. If you are interested in learning more about how to build an application like this one, read our step-by-step [Build a store locator](/help/tutorials/building-a-store-locator) tutorial.
{{</div>}}

## How web apps work

A web mapping library allows you to add a map to a webpage and define the data it contains, its appearance, and a variety of functionality. Think of it like a toolbox filled with many different map-making tools that can be used together to build beautiful and interactive custom experiences.

### Mapbox GL JS

[Mapbox GL JS](https://www.mapbox.com/mapbox-gl-js) is a JavaScript library for building web applications with our modern mapping technology. This guide walks through some of Mapbox GL JS's essential functions and common patterns, highlighting some of the core concepts that distinguish Mapbox GL JS from other map libraries. For those with experience using [Leaflet](/help/glossary/leaflet/), [Mapbox.js](/help/glossary/mapbox-js/), or OpenLayers, the next few sections will introduce some of the differences in Mapbox GL JS as well as features that should look familiar.

#### Client-side rendering

At the heart of Mapbox GL JS is client-side rendering. In web apps using Mapbox GL JS, maps are rendered dynamically by combining [vector tiles](/help/glossary/vector-tiles/) with [style rules](https://www.mapbox.com/mapbox-gl-style-spec/) using JavaScript and WebGL. Rendering maps in the browser rather than on a server makes it possible to change the map's style and the data it displays dynamically and in response to user interaction.

#### The camera

The camera is the map's field of view. While the viewpoint in systems like Leaflet or Mapbox.js is determined by the map's centerpoint and zoom level, Mapbox GL JS also includes parameters like pitch and bearing for adjusting the map's perspective.

* **Center**: in longitude, latitude order.
* **Zoom**: any number within the zoom range, including decimals. For example, 1.5 or 6.2 are valid zoom levels.
* **Bearing**: a value between 0 and 360 degrees that determines the map's bearing, or rotation.
* **Pitch**: a value between 0 and 60 degrees that determines the map's tilt, or pitch.

Here's an example of combining bearing and zoom:

{{
  <DemoIframe src="/help/demos/gl-js-fundamentals/bearing_and_zoom.html" />
}}

#### Layers

Traditional JavaScript map libraries often have two distinct categories
of what are called "[layers](/help/glossary/layer/)": **[baselayers](/help/glossary/baselayer/)**, or image tiles that provide the foundation of the map, and **overlays**, which are often vector data like GeoJSON that are displayed on top of baselayers, sometimes obscuring details like labels.

Mapbox GL JS has **no distinction between baselayers and overlay layers**. This means
that map details like labels and icons and elements like streets and buildings
can be modified with JavaScript, like overlays in earlier mapping libraries. Each layer provides rules about how the renderer should draw certain data in the browser, and the renderer uses these layers to draw the map on the screen.

#### Mapbox GL JS and Mapbox GL Native

[Mapbox GL JS](https://www.mapbox.com/mapbox-gl-js) and [Mapbox GL Native](https://github.com/mapbox/mapbox-gl-native) are two different projects for rendering maps build to the [Mapbox Style Specification](https://www.mapbox.com/mapbox-gl-style-spec). They are similar, but are used for different purposes and do not have 100% feature parity.

- **Mapbox GL JS** is a JavaScript library for making maps for the web. It can read the Mapbox Style Specification and uses WebGL to render your maps in modern browsers.
- **Mapbox GL Native** is the backbone of the Mapbox Maps SDKs for [iOS](https://www.mapbox.com/ios-sdk) and [Android](https://www.mapbox.com/android-sdk). It supports the iOS and Android mobile platforms using OpenGL ES.

### Mapbox.js

{{
  <LegacyNote
    legacyProduct='Mapbox.js'
    alternativeResource={{
      title: 'the Mapbox GL JS documentation',
      link: 'https://docs.mapbox.com/mapbox-gl-js/overview/'
    }}
  />
}}

Mapbox.js is a **web mapping library** that extends the popular [Leaflet.js](/help/glossary/leaflet) library. Mapbox.js boasts the power of Leaflet.js, but is also heavily integrated with the Mapbox stack. You can learn more about Mapbox.js in its [API documentation](https://www.mapbox.com/mapbox.js/api/).

## Creating a web app

To create a web map, you'll need to have some familiarity with HTML, CSS, and JavaScript. If you are new to web maps, explore our [tutorials](/help/tutorials/) to help you get started.

### Mapbox GL JS

Before getting started coding up your Mapbox GL JS map, you'll need to include the relevant JavaScript and CSS files in your webpage. Mapbox provides hosted versions of each that you can include in the `<head>` of your HTML file:

``` html
<script src='https://api.mapbox.com/mapbox-gl-js/{{constants.VERSION_MAPBOXGLJS}}/mapbox-gl.js'></script>
<link href='https://api.mapbox.com/mapbox-gl-js/{{constants.VERSION_MAPBOXGLJS}}/mapbox-gl.css' rel='stylesheet' />
```

The basis of every Mapbox GL JS project is the `mapboxgl.Map` class. The example code in this section demonstrates the minimum you need to add a map to your page.

<div class='fr pl12' style='width:50%'>
<pre>
var map = new mapboxgl.Map({
  container: 'map',
  style: 'mapbox://styles/mapbox/streets-v{{constants.VERSION_STREETS_STYLE}}',
  center: [-74.50, 40],
  zoom: 9
});
</pre>
</div>

- **Container**: This is the HTML element where you would like to place your map. In the example above, it is an element with `id="map"`.
- **Style**: The map loads a style via the URL `mapbox://styles/mapbox/streets-v{{constants.VERSION_STREETS_STYLE}}`. This is a URL to a remote file that the map will download to determine the [tilesets](/help/glossary/tileset/) it includes and how they are styled for the end-user. Mapbox GL JS permits URLs instead of literal data in several places, including data sources. Consider using a style with [style-optimized vector tiles](/help/glossary/style-optimized-vector-tiles/) for more performant maps.
- **Center**: Where Mapbox GL JS handles coordinates as arrays (here `[-74.50, 40]`), it assumes that the coordinates are in [`longitude, latitude`](/help/glossary/lat-lon/) order (versus `latitude, longitude` in Leaflet and Mapbox.js). This order corresponds to the order of coordinates in GeoJSON and every other geospatial format, as well as math's X, Y ordering.
- **Zoom**: The zoom level at which the map should be initialized. With Mapbox GL JS, can be a decimal value.

#### Adding layers to the map

You can add layers to the map using the `addLayer()` method. [`addLayer`](https://www.mapbox.com/mapbox-gl-js/api/#Map.addLayer) has only one required parameter: a Mapbox style layer object. It also accepts an optional `before` parameter, which is the ID of an existing layer to insert the new layer before. If you omit this argument, then  the renderer will draw the layer on top of the map. The following sections describe the elements of a Mapbox style layer object.

##### Asynchronous

<div class='fr pl12' style='width:50%'>
<pre>
map.on('load', function() {
  map.addLayer({
    id: 'terrain-data',
    type: 'line',
    source: {
      type: 'vector',
      url: 'mapbox://mapbox.mapbox-terrain-v2'
    },
    'source-layer': 'contour'
  });
});
</pre>
</div>

Since these resources are **remote**, they are **asynchronous**. So code that connects to Mapbox GL JS often uses event binding to change the map at the right time. For instance:

The above code uses the `map.on('load', function() {` code to call `map.addLayer` only after the map's resources, including the style, have been loaded. If it were to run the `map.addLayer` method immediately, it would trigger an error because the style to which you would like to add a layer would not yet exist.

##### Specifying a source

You will need to define a source when you add a new layer. A source accepts a `type` and a `url` (a GeoJSON source will not have a `url`). There are five types of sources, each with its own properties:

- [vector tiles](https://www.mapbox.com/mapbox-gl-style-spec/#sources-vector)
- [raster tiles](https://www.mapbox.com/mapbox-gl-style-spec/#sources-raster)
- [GeoJSON](https://www.mapbox.com/mapbox-gl-style-spec/#sources-geojson)
- [image](https://www.mapbox.com/mapbox-gl-style-spec/#sources-image)
- [video](https://www.mapbox.com/mapbox-gl-style-spec/#sources-video)

Tilesets can include multiple subsets of data called [source layers](/help/glossary/source-layer/) (the Mapbox Streets tileset contains source layers for roads, parks, etc). To make sure your layers are referencing the correct source layers, your layer object also needs to include a `source-layer` (often the name of the original file). See this example:

{{
  <Note title='addSource()' imageComponent={<BookImage />}>
    <p>You can also add sources using the Mapbox GL JS <code>addSource()</code> method. There is no difference in map performance when using this alternative method, but it is sometimes preferable to keep code more readable. Read more about this method in the <a href="https://www.mapbox.com/mapbox-gl-js/api/#Map#addSource">Mapbox GL JS documentation</a>.</p>
  </Note>
}}

```js
map.on('load', function() {
  map.addLayer({
    id: 'rpd_parks',
    type: 'fill',
    source: {
      type: 'vector',
      url: 'mapbox://mapbox.3o7ubwm8'
    },
    'source-layer': 'RPD_Parks'
  });
});
```

For more information on each source type, explore the Sources section of the [Mapbox Style Specification](https://www.mapbox.com/mapbox-gl-style-spec#sources).

##### Specifying layout and paint properties

Layers feature two special properties that enable data styling: [`paint`](https://www.mapbox.com/mapbox-gl-style-spec/#paint) and [`layout`](https://www.mapbox.com/mapbox-gl-style-spec/#layout). These are used to define how data will be rendered on the map. `layout` properties refer to placement and visibility, among other high-level preferences, and are applied early in the rendering process. `paint` properties are more fine-grained style attributes like opacity, color, and translation. They are less processing-intensive and are rendered later.

The following code adds a layer to the map to style the parks data with a green fill.

{{
  <Note title='addLayer()' imageComponent={<BookImage />}>
    <p>If you added your source using the alternative <code>addSource()</code> method, you will need to include the source id as the <code>source</code> in <code>addLayer()</code>. Read more about this in the <a href="https://www.mapbox.com/mapbox-gl-js/api/#Map#addLayer">Mapbox GL JS API documentation.</a></p>
  </Note>
}}

```js
map.on('load', function() {
  map.addLayer({
    id: 'rpd_parks',
    type: 'fill',
    source: {
      type: 'vector',
      url: 'mapbox://mapbox.3o7ubwm8'
    },
    'source-layer': 'RPD_Parks',
    layout: {
      visibility: 'visible'
    },
    paint: {
      'fill-color': 'rgba(61,153,80,0.55)'
    }
  });
});
```

The final product: a map zoomed to San Francisco with a parks layer with a green fill. The layer is based on a vector source of the city's park lands data.

See the [tutorials section](/help/tutorials/) for more Mapbox GL JS resources.

### Mapbox.js

{{
  <LegacyNote
    legacyProduct='Mapbox.js'
    alternativeResource={{
      title: 'the Mapbox GL JS documentation',
      link: 'https://docs.mapbox.com/mapbox-gl-js/overview/'
    }}
  />
}}

#### Add a map to the page

The core function of Mapbox.js is adding a map to your HTML page. Using one line of JavaScript, you can add a map to your webpage with a basemap that pans and zooms, set to a [specific location and zoom level](https://www.mapbox.com/mapbox.js/api/{{constants.VERSION_MAPBOXJS}}/l-map-class/#map-options).

See our example to [add a map with Mapbox.js](https://www.mapbox.com/mapbox.js/example/v1.0.0/).

#### Add and style custom data

If you want to add your own data to your Mapbox.js map, you can! Mapbox.js supports a few different formats, including [GeoJSON](/help/glossary/geojson). You can then style your GeoJSON data by adding style properties to the GeoJSON in the [simplestyle specification](/help/glossary/simplestyle/) or by using the built-in `setStyle` method.

See [this example](https://www.mapbox.com/mapbox.js/example/v1.0.0/single-marker/) for how to add GeoJSON data to a map and style it using the simplestyle specification.

## Extend your web app with plugins

Mapbox GL JS and Mapbox.js both support a rich ecosystem of plugins you can use to extend the functionality of your web map. There are plugins for adding interactive drawing tools, adding inset maps, integrating with the Mapbox Geocoding API and the Mapbox Directions API, and more! Explore the [Mapbox GL JS plugins page](https://www.mapbox.com/mapbox-gl-js/plugins) and the [Mapbox.js plugins page](https://www.mapbox.com/mapbox.js/plugins/) for more information.

## Use Mapbox GL JS with React

Mapbox GL JS can be used with various JavaScript frameworks, including [React](https://facebook.github.io/react/). To learn more about using Mapbox GL JS with React, see our [Mapbox react examples on GitHub](https://github.com/mapbox/mapbox-react-examples).
