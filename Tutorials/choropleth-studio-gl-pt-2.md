---
title: "Make a choropleth map, part 2: add interactivity"
description: Publish your style with Mapbox GL JS, create a legend, and add interactive elements.
thumbnail: choroplethStudioGlPt2
level: 2
topics:
- uploads
- map design
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
contentType: tutorial
---

In [part 1](/help/tutorials/choropleth-studio-gl-pt-1), you styled US population density data in the Mapbox Studio style editor and published a new style. In part 2, you will make this style come to life with interactions using Mapbox GL JS.

{{
  <DemoIframe src="/help/demos/choropleth-studio-gl/demo-five.html" />
}}

## How Mapbox Studio and Mapbox GL JS work together

In the last guide, you used the Mapbox Studio style editor to design your map and create a style. But what did the software produce when you clicked Publish?

### What is a style?

The style is the most important part of making a web map: it contains all the rules for what features to draw on the webpage and how to draw them. Both Mapbox Studio and Mapbox GL JS interact directly with your style: the Mapbox Studio style editor is a visual interface for creating the style, and Mapbox GL JS is used to add the style to a webpage and interact with it directly by adding and changing the layers and sources in response to browser events.

A [map style](/help/glossary/style) is a JSON object in the [Mapbox Style Specification](https://www.mapbox.com/mapbox-gl-style-spec/) that contains all the things the browser needs to draw your map correctly. Its main parts are:

- **`sources`**: links to all the data that will be styled on the map. When creating a style with the Mapbox Studio style editor, sources are raster and vector tilesets in your Mapbox account.
- **`sprite`**: a link to all the images and icons that are used in the style.
- **`glyphs`**: a link to all the fonts that are used in the style.
- **`layers`**: a list of rules for how the data in `sources` should be displayed on the map.

When you added the population density data to your Mapbox Studio style in part 1, a link to it was also added to the list of sources in a style object (we normally refer to these as "styles"). Similarly, when you added the population density layer and gave it styling rules for the each category of data, that layer was also added to the list of layers in your style.

## Get started

Here's what you need to get started:

- [**An access token**](/help/glossary/access-token). You can find your access tokens on your [Account page](https://www.mapbox.com/account/).
- The [**style URL**](/help/glossary/style-url) for your style. From your [Styles](https://www.mapbox.com/studio) page, click on the **Menu {{<Icon name='menu' inline={true} />}}** button next to your population density style and then click the {{<Icon name='clipboard' inline={true} />}} clipboard icon to copy the **Style URL**.
- [**Mapbox GL JS**](https://www.mapbox.com/mapbox-gl-js). The Mapbox JavaScript API for building web maps.
- **A text editor**. You'll be writing HTML, CSS, and JavaScript after all.

## Create a webpage

Open your text editor and create a file called `index.html`. Set up the document by adding Mapbox GL JS and its associated CSS file in the header:

```html
<script src='https://api.mapbox.com/mapbox-gl-js/{{constants.VERSION_MAPBOXGLJS}}/mapbox-gl.js'></script>
<link href='https://api.mapbox.com/mapbox-gl-js/{{constants.VERSION_MAPBOXGLJS}}/mapbox-gl.css' rel='stylesheet' />
```

Next, markup the page to create a map container, an information box, and a legend:

```html
<div id='map'></div>
<div class='map-overlay' id='features'><h2>US population density</h2><div id='pd'><p>Hover over a state!</p></div></div>
<div class='map-overlay' id='legend'></div>
```

You will also want to apply some CSS to visualize what the layout looks like. This is particularly important for the `map` div, which won't show up on the page until you give it a `height`:

```css
body {
  margin: 0;
  padding: 0;
}

h2,
h3 {
  margin: 10px;
  font-size: 1.2em;
}

h3 {
  font-size: 1em;
}

p {
  font-size: 0.85em;
  margin: 10px;
  text-align: left;
}

/**
* Create a position for the map
* on the page */
#map {
  position: absolute;
  top: 0;
  bottom: 0;
  width: 100%;
}

/**
* Set rules for how the map overlays
* (information box and legend) will be displayed
* on the page. */
.map-overlay {
  position: absolute;
  bottom: 0;
  right: 0;
  background: rgba(255, 255, 255, 0.8);
  margin-right: 20px;
  font-family: Arial, sans-serif;
  overflow: auto;
  border-radius: 3px;
}

#features {
  top: 0;
  height: 100px;
  margin-top: 20px;
  width: 250px;
}

#legend {
  padding: 10px;
  box-shadow: 0 1px 2px rgba(0, 0, 0, 0.1);
  line-height: 18px;
  height: 150px;
  margin-bottom: 40px;
  width: 100px;
}

.legend-key {
  display: inline-block;
  border-radius: 20%;
  width: 10px;
  height: 10px;
  margin-right: 5px;
}
```

In the next step, you will add the map to your page and the project will start taking shape.

## Initialize map

Now that you've added structure to the page, you can start writing some JavaScript! The first thing you'll need to do is add your access token. Without this, the rest of the code will not work. _Note: all the following code should be between `script` tags._:

```js
mapboxgl.accessToken = '{{ <UserAccessToken /> }}';
```

Now that you've added the structure of the page, you can add a map object into the `map` div. Be sure to replace `your-style-url` with the [style URL](/help/glossary/style-url) for the style you created in part 1 of this guide -- otherwise the code won't work!

```js
var map = new mapboxgl.Map({
  container: 'map', // container id
  style: 'your-style-url' // replace this with your style URL
});
```

{{
  <DemoIframe src="/help/demos/choropleth-studio-gl/demo-two.html" />
}}

## Add additional information

With some projects, this is where you'd stop: you put a map on a page! But for this map, you will add two pieces of additional information that will make the map even more useful: a legend and an information window that shows the population density for whatever state the cursor is hovering on.

### The 'load' event

{{
  <Note title='What is a callback?' imageComponent={<BookImage />}>
    <p>Initializing the map on the page does more than create a container in the <code>map</code> div. It also tells the browser to request the Mapbox Studio style you created in part 1. This can take variable amounts of time depending on how quickly the Mapbox server can respond to that request, and everything else you're going to add in the code relies on that style being loaded onto the map. As such, it's important to make sure the style is loaded before any more code is executed.</p><p>Fortunately, the map object can tell your browser about certain events that occur when the map's state changes. One of these events is <code>load</code>, which is emitted when the style has been loaded onto the map. Through the <code>map.on</code> method, you can make sure that none of the rest of your code is executed until that event occurs by placing it in a <a href='https://github.com/maxogden/art-of-node#callbacks'>callback function</a> that is called when the <code>load</code> event occurs.</p>
  </Note>
}}

To make sure the rest of the code can execute, it needs to live in a *callback function* that is executed when the map is finished loading.

```js
map.on('load', function() {
  // the rest of the code will go in here
});
```

### Create arrays of intervals and colors

Creating a list of the stops you used when styling your layer that contains state data will allow us to add a legend to our map in a later step.

_Remember: this code goes inside of the `load` callback function!_

```js
var layers = ['0-10', '10-20', '20-50', '50-100', '100-200', '200-500', '500-1000', '1000+'];
var colors = ['#FFEDA0', '#FED976', '#FEB24C', '#FD8D3C', '#FC4E2A', '#E31A1C', '#BD0026', '#800026'];
```

### Add a legend

The following code adds a legend to the map. To do so, it iterates through the list of layers you defined above and adds a legend element for each one based on the name of the layer and its color.

```js
for (i = 0; i < layers.length; i++) {
  var layer = layers[i];
  var color = colors[i];
  var item = document.createElement('div');
  var key = document.createElement('span');
  key.className = 'legend-key';
  key.style.backgroundColor = color;

  var value = document.createElement('span');
  value.innerHTML = layer;
  item.appendChild(key);
  item.appendChild(value);
  legend.appendChild(item);
}
```

{{
  <DemoIframe src="/help/demos/choropleth-studio-gl/demo-three.html" />
}}

### Add the information window

When the cursor is hovering over a state, the information window should show the population density information for that state. If the cursor is not hovering over a state, the information window should say, "Hover over a state!"

To do this, add a listener for the `mousemove` event, identify which state is at the location of the cursor if any, and update the information window:

```js
map.on('mousemove', function(e) {
  var states = map.queryRenderedFeatures(e.point, {
    layers: ['statedata']
  });

  if (states.length > 0) {
    document.getElementById('pd').innerHTML = '<h3><strong>' + states[0].properties.name + '</strong></h3><p><strong><em>' + states[0].properties.density + '</strong> people per square mile</em></p>';
  } else {
    document.getElementById('pd').innerHTML = '<p>Hover over a state!</p>';
  }
});
```

{{
  <DemoIframe src="/help/demos/choropleth-studio-gl/demo-four.html" />
}}

## Final touches

Almost done! A couple last little steps:

### Cursor

Add a single line of code to give the map the default pointer cursor.

```js
map.getCanvas().style.cursor = 'default';
```

### Map bounds

Make sure the map shows the continental U.S. when it's loaded by setting the bounds of the map on load:

```js
map.fitBounds([[-133.2421875, 16.972741], [-47.63671875, 52.696361]]);
```

## Mission complete

You have created an interactive choropleth map!

{{
  <DemoIframe src="/help/demos/choropleth-studio-gl/demo-five.html" />
}}

Nice job! For more things you can do with Mapbox Studio, explore the [Mapbox Studio Manual](https://www.mapbox.com/studio-manual/). For more information on Mapbox GL JS and how it works, read the [How web apps work](/help/how-mapbox-works/web-apps/) guide.
