---
title: Create interactive hover effects with Mapbox GL JS
description: Use feature state and expressions with Mapbox GL JS to dynamically style individual features in a map that shows earthquakes from the past week.
thumbnail: featureStateFinal
topics:
- web apps
level: 2
language:
- JavaScript
prereq: Familiarity with front-end development concepts.
prependJs:
  - "import Note from '@mapbox/dr-ui/note';"
  - "import BookImage from '@mapbox/dr-ui/book-image';"
  - "import Icon from '@mapbox/mr-ui/icon';"
  - "import DemoIframe from '@mapbox/dr-ui/demo-iframe';"
  - "import UserAccessToken from '../../components/user-access-token';"
  - "import * as constants from '../../constants';"
  - "import AppropriateImage from '../../components/appropriate-image';"
contentType: tutorial
---
<!--copyeditor ignore magnitude -->
In this tutorial, you will create a map that shows the location of earthquakes that have happened in the last week. You will use [expressions](https://docs.mapbox.com/mapbox-gl-js/style-spec/#expressions) to set a style for the earthquake features according to the magnitude of the earthquake. Finally, you will use [feature state](https://docs.mapbox.com/mapbox-gl-js/style-spec/#expressions-feature-state) to apply these styles to the earthquake features when a user mouses over the feature and remove them when a user mouses away.  

{{
  <DemoIframe src="/help/demos/create-interactive-hover-effects-with-mapbox-gl-js/index.html" />
}}

Feature state is a set of user-defined attributes that can be dynamically assigned to a feature on the map. Feature state is used with [expressions](https://docs.mapbox.com/help/glossary/expression/) to style the [features](https://www.mapbox.com/help/define-features/) of a vector or GeoJSON source in either a dataset or tileset. Each feature in the source must have a unique numeric `id` in order for feature state to work correctly. If you are adding a GeoJSON source at runtime, which is what you will do in this tutorial, you can use the  `generateId` option in [`map.addSource()`](https://docs.mapbox.com/mapbox-gl-js/api/#map#addsource) to add an `id` to each feature. For vector sources or GeoJSON sources that are added before runtime, you must set a unique `id` for each feature before the source is added to the map.

You can think of feature state as a switch that turns a fan on or off. You will use feature state to define what the switch is, and expressions to set the style. In this case, the trigger is a user mousing over or away from a feature, which will update the style of the feature based on the rules set by the expressions.

<!--copyeditor ignore magnitude -->
Feature state allows you to update the styling of a map layer's individual features based on user interaction, without needing to re-render the underlying geometry and data after each interaction event. In this tutorial, the feature state trigger will be a user hovering over an earthquake feature, and you will use feature state to update the radius size and the color of the feature based on its magnitude value.  

## Getting started
To complete this tutorial, you will need:
<!--copyeditor ignore magnitude -->
- **A Mapbox access token.** Your Mapbox access tokens are on your [Account page](https://account.mapbox.com/).
- **Mapbox GL JS.** [Mapbox GL JS](https://docs.mapbox.com/mapbox-gl-js/overview/) is a JavaScript API for building web maps.
- **A text editor.** Use the text editor of your choice for writing HTML, CSS, and JavaScript.
- **The USGS Earthquake Catalog API.** You will use the [USGS Earthquake Catalog API](https://earthquake.usgs.gov/fdsnws/event/1/) to retrieve information about all earthquakes with a magnitude of one or more that have happened within the past week.

## Create a map
To get started, you will create a map using [Mapbox GL JS](https://docs.mapbox.com/mapbox-gl-js/api/). Open your text editor and create a new file named `index.html`. Set up this new HTML file by pasting the following code into your text editor:

```html
<!DOCTYPE html>
<html>

<head>
  <meta charset='utf-8' />
  <title>Create interactive hover effects with Mapbox GL JS</title>
  <meta name='viewport' content='initial-scale=1,maximum-scale=1,user-scalable=no' />
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
      container: 'map', // Specify the container ID
      style: 'mapbox://styles/mapbox/outdoors-v{{constants.VERSION_OUTDOORS_STYLE}}', // Specify which map style to use
      center: [-122.44121, 37.76132], // Specify the starting position [lng, lat]
      zoom: 3.5 // Specify the starting zoom
    });
  </script>
  
</body>
</html>        
```

This code creates the structure of the page. It imports Mapbox GL JS in the `<head>` of the page, which allows you to use Mapbox GL JS functionality and style in your web app.

This code contains a `<div>` element with the ID `map` in the `<body>` of the page. This `<div>` is the container in which the map will be displayed on the page.

Save your changes. Open the HTML file in your browser to see the rendered map, which is centered on the western United States.

{{
<AppropriateImage imageId="featureStateBaseMap" alt="Basemap using the Mapbox Outdoors style" />
}}

## Add the sidebar
<!--copyeditor ignore magnitude -->
In the `<body>` of your HTML, add a new `<div>`. This `<div>` will be used to display an individual earthquake's magnitude, location, and the time that it happened:

```html
<div class='quakeInfo'>
  <div><strong>Magnitude:</strong>&nbsp;<span id='mag'></span></div>
  <div><strong>Location:</strong>&nbsp;<span id='loc'></span></div>
  <div><strong>Date:</strong>&nbsp;<span id='date'></span></div>
</div>
```

To style the new `<div>`, add the following CSS to the `<style>` section of your HTML:

```css
.quakeInfo {
  position: absolute;
  font-family: sans-serif;
  margin-top: 5px;
  margin-left: 5px;
  padding: 5px;
  width: 30%;
  border: 2px solid black;
  font-size: 14px;
  color: #222;
  background-color: #fff;
  border-radius: 3px;
}
```

Finally, create three new variables that you will use to target the new `<span>`s using their IDs. Add the following code to your JavaScript, above the closing `</script>` tag:

```js
var magDisplay = document.getElementById('mag');
var locDisplay = document.getElementById('loc');
var dateDisplay = document.getElementById('date');
```
<!--copyeditor ignore magnitude -->
Save your work and refresh the page. The new sidebar will be on the left side of the page. In an upcoming step, you will use the `<span>`s that you created to display the magnitude, location, and time of the earthquakes in the sidebar.  

{{
<AppropriateImage imageId="featureStateSidebar" alt="Basemap using the Mapbox Outdoors style, with a styled sidebar with the words Magnitude, Location, and Date" />
}}

## Add the earthquake source
<!--copyeditor ignore magnitude -->
The Mapbox GL JS [`addSource` instance](https://docs.mapbox.com/mapbox-gl-js/api/#map#addsource) lets you add a new data source to a map. In this case, you will use data from the [USGS Earthquake Catalog API](https://earthquake.usgs.gov/fdsnws/event/1/), which returns information about recent earthquakes, including the magnitude, location, and the time at which the earthquake happened.

By default, the Earthquake Catalog API returns all events from the prior 30 days. But for this web app, you will instead return events from the past seven days using the optional `starttime` parameter. You will use the [JavaScript `Date` constructor](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date) to get the date seven days ago as an [ISO 8601 timestamp](https://www.iso.org/iso-8601-date-and-time-format.html), as required by the USGS Earthquake Catalog API. Add the following JavaScript to your file:

```js
var today = new Date();
// Use JavaScript to get the date a week ago
var priorDate = new Date().setDate(today.getDate() - 7);
// Set that to an ISO8601 timestamp as required by the USGS earthquake API
var priorDateTs = new Date(priorDate);
var sevenDaysAgo = priorDateTs.toISOString();
```   

You will use the `sevenDaysAgo` variable in a call to the Earthquake Catalog API. (If you use a time-specific JavaScript library like [Moment.js](https://momentjs.com/), getting the current date minus seven days will take fewer steps, but for the purposes of this tutorial the steps are shown in plain JavaScript.)

For this web app, you will use the Earthquake Catalog API's optional `format` parameter to return the data as GeoJSON. You will also restrict the results to earthquakes with a magnitude of one or higher by using the optional `eventtype` and `minmagnitude` parameters.

With these optional parameters, the USGS Earthquake Catalog API query will be:
```
"https://earthquake.usgs.gov/fdsnws/event/1/query?format=geojson&eventtype=earthquake&minmagnitude=1&starttime=" + sevenDaysAgo
```

To add results from a call to the Earthquake Catalog API to your app as a source, you will wrap `addSource` inside a `map.on('load')` function so that the new source is not loaded before the map is rendered. Add the following code to your JavaScript:

```js
map.on('load', function() {

  map.addSource('earthquakes', {
    'type': 'geojson',
    'data': 'https://earthquake.usgs.gov/fdsnws/event/1/query?format=geojson&eventtype=earthquake&minmagnitude=1&starttime=' + sevenDaysAgo,
    'generateId': true // This ensures that all features have unique IDs
  });
  
});  
```

{{<Note title="Setting unique IDs for features" imageComponent={<BookImage />}>}}
Feature state relies on each feature having a numeric `id` that is unique across the source or source layer.

If you are using a GeoJSON source that is generated at runtime, as with the results from the Earthquake Catalog API in this tutorial, you can add an `id` to each feature by setting the `generateId` property in `map.addSource()` to `true`. This generates an `id` for each feature in the new source, based on the feature's index in the source data.

The `generateId` method only works for GeoJSON sources that are added at runtime. For tilesets, or for GeoJSON sources that are added before runtime, unique `id`s must be set for each feature before the source is added to the map.  
{{</Note>}}

In the next step, you will add a style layer that uses the source `earthquakes` to the map.  

## Add the earthquake layer
The Mapbox GL JS [`addLayer` instance](https://docs.mapbox.com/mapbox-gl-js/api/#map#addlayer) creates a new map layer, which defines styling for data from a specified source. In this case, the data is coming from the `earthquakes` source that you created in the last step.

Add the following `addLayer` function inside `map.on('load')`, below the `addSource` function you wrote in the last step:

```js
map.addLayer({
  'id': 'earthquakes-viz',
  'type': 'circle',
  'source': 'earthquakes',
  'paint': {
    'circle-stroke-color': '#000',
    'circle-stroke-width': 1,
    'circle-color': '#000'
  }
});
```
<!--copyeditor ignore magnitude -->
Save your work and refresh the page in your browser. You will see that the new `earthquake-viz` layer draws each earthquake as a black dot, as specified in the `paint` property. In the next step, you will use:
- **`feature-state`** to change the style of an individual feature when the user hovers over it
- **`interpolate`, `linear`, and `get` expressions** to determine what that new style should be, based on the magnitude of the earthquake

{{
<AppropriateImage imageId="featureStateAddLayer" alt="Basemap with black circles representing the features in the new earthquake-viz layer" />
}}

## Style the earthquakes using feature state
Feature state can be used to style any of the paint properties that support [data-driven styling](https://docs.mapbox.com/help/glossary/data-driven-styling/) with values from these attributes. Learn more about paint property support levels in the [Mapbox style specification](https://www.mapbox.com/mapbox-gl-js/style-spec/#layers). In feature state, features are identified by their `id` property, which must be unique across a source or source layer. When you used `addSource` to add the earthquake data as a source, you set `'generateId': true`, which ensures that all features have unique IDs.

In this case, you will use feature state to change the color and radius size of the circle marking a feature based on an attribute (`hover`) with a boolean value. Then you will define the `hover` attribute using [`setFeatureState`](https://docs.mapbox.com/mapbox-gl-js/api/#map#setfeaturestate).
<!--copyeditor ignore magnitude -->
Update `addLayer` to use feature state for `circle-radius` and `circle-color`. The updated code also uses the expressions [`interpolate` operator](https://docs.mapbox.com/mapbox-gl-js/style-spec/#expressions-interpolate) to set the `circle-radius` and the `circle-color` according to the magnitude of the selected earthquake feature.

```js
map.addLayer({
  'id': 'earthquakes-viz',
  'type': 'circle',
  'source': 'earthquakes',
  'paint': {
    // The feature-state dependent circle-radius expression will render
    // the radius size according to its magnitude when
    // a feature's hover state is set to true
    'circle-radius': [
      'case',
      ['boolean',
        ['feature-state', 'hover'],
        false
      ],
      [
        'interpolate', ['linear'],
        ['get', 'mag'],
        1, 8,
        1.5, 10,
        2, 12,
        2.5, 14,
        3, 16,
        3.5, 18,
        4.5, 20,
        6.5, 22,
        8.5, 24,
        10.5, 26
      ],
      5
    ],
    'circle-stroke-color': '#000',
    'circle-stroke-width': 1,
    // The feature-state dependent circle-color expression will render
    // the color according to its magnitude when
    // a feature's hover state is set to true
    'circle-color': [
      'case',
      ['boolean',
        ['feature-state', 'hover'],
        false
      ],
      [
        'interpolate', ['linear'],
        ['get', 'mag'],
        1, '#fff7ec',
        1.5, '#fee8c8',
        2, '#fdd49e',
        2.5, '#fdbb84',
        3, '#fc8d59',
        3.5, '#ef6548',
        4.5, '#d7301f',
        6.5, '#b30000',
        8.5, '#7f0000',
        10.5, '#000'
      ],
      '#000'
    ]
  }
});
```

## Define the hover attribute

Next, you will use [`setFeatureState`](https://docs.mapbox.com/mapbox-gl-js/api/#map#setfeaturestate) to define the `hover` attribute. In order to trigger the feature state changes when a user mouses over an earthquake feature, you will wrap `setFeatureState` in a `map.on('mousemove')` function.

The following code creates several new variables, each of which will be updated for every `map.on('mousemove')` event:
<!--copyeditor ignore magnitude -->
- `quakeID`: This variable will be set to the `id` of the current feature, which allows you to target each earthquake individually.
- `quakeMagnitude`: The returned magnitude of the current feature.
- `quakeLocation`: The returned location of the current feature.
- `quakeDate`: The returned date of the current feature.

Paste the following code into your JavaScript, above the final `</script>` tag:

```js
var quakeID = null;

map.on('mousemove', 'earthquakes-viz', (e) => {

  map.getCanvas().style.cursor = 'pointer';
  // Set variables equal to the current feature's magnitude, location, and time
  var quakeMagnitude = e.features[0].properties.mag;
  var quakeLocation = e.features[0].properties.place;
  var quakeDate = new Date(e.features[0].properties.time);

  // Check whether features exist
  if (e.features.length > 0) {
    // Display the magnitude, location, and time in the sidebar
    magDisplay.textContent = quakeMagnitude;
    locDisplay.textContent = quakeLocation;
    dateDisplay.textContent = quakeDate;

    // If quakeID for the hovered feature is not null,
    // use removeFeatureState to reset to the default behavior
    if (quakeID) {
      map.removeFeatureState({
        source: "earthquakes",
        id: quakeID
      });
    }

    quakeID = e.features[0].id;

    // When the mouse moves over the earthquakes-viz layer, update the
    // feature state for the feature under the mouse
    map.setFeatureState({
      source: 'earthquakes',
      id: quakeID,
    }, {
      hover: true
    });

  }
});
```
<!--copyeditor disable magnitude -->
Save your work and refresh your browser page. Now, when you mouse over an earthquake feature, two things will happen:
- The magnitude, location, and date of the earthquake will be displayed in the sidebar.
- The styling of the circle that marks the feature will change based on the returned `mag` property.

{{
<AppropriateImage imageId="featureStateFinal" alt="Screenshot showing the basemap that demonstrates how the feature state expression changes the styling of features" />
}}

When you move your mouse away from an earthquake feature, though, the circle will stay the same size and color, and the sidebar will continue displaying that feature's information, until you mouse over another feature. You will fix this in the next step.

## Reset the feature state
The final step in creating this web app is to update the feature state of an earthquake feature when the user mouses away from it. You will also use this `map.on('mouseleave')` function to reset the sidebar display when the user mouses away.  

Paste the following code into your JavaScript above the closing `</script>` tag:

```js
map.on("mouseleave", "earthquakes-viz", function() {
  if (quakeID) {
    map.setFeatureState({
      source: 'earthquakes',
      id: quakeID
    }, {
      hover: false
    });
  }
  
  quakeID = null;
  // Remove the information from the previously hovered feature from the sidebar
  magDisplay.textContent = '';
  locDisplay.textContent = '';
  dateDisplay.textContent = '';
  // Reset the cursor style
  map.getCanvas().style.cursor = '';
});
```

Save your work, then refresh the page in your browser. Now when you mouse over an earthquake feature and then move the mouse away from it, the sidebar will reset until you mouse over a new earthquake feature.

## Final product
<!--copyeditor ignore magnitude -->
You have created a web app that uses feature state to dynamically style earthquake features on a map, based on the earthquake's magnitude.

{{
  <DemoIframe src="/help/demos/create-interactive-hover-effects-with-mapbox-gl-js/index.html" />
}}

The final HTML file will look like the following:

```html
<!DOCTYPE html>
<html>

<head>
  <meta charset='utf-8' />
  <title>Create interactive hover effects with Mapbox GL JS</title>
  <meta name='viewport' content='initial-scale=1,maximum-scale=1,user-scalable=no' />
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

    .quakeInfo {
      position: absolute;
      font-family: sans-serif;
      margin-top: 5px;
      margin-left: 5px;
      padding: 5px;
      width: 30%;
      border: 2px solid black;
      font-size: 14px;
      color: #222;
      background-color: #fff;
      border-radius: 3px;
    }
  </style>
</head>

<body>

  <div id='map'></div>
  <div class='quakeInfo'>
    <div><strong>Magnitude:</strong> <span id='mag'></span></div>
    <div><strong>Location:</strong> <span id='loc'></span></div>
    <div><strong>Date:</strong> <span id='date'></span></div>
  </div>

  <script>
    mapboxgl.accessToken = '{{ <UserAccessToken /> }}';
    var map = new mapboxgl.Map({
      container: 'map', // Specify the container ID
      style: 'mapbox://styles/mapbox/outdoors-v{{constants.VERSION_OUTDOORS_STYLE}}', // Specify which map style to use
      center: [-122.44121, 37.76132], // Specify the starting position [lng, lat]
      zoom: 3.5 // Specify the starting zoom
    });

    // Target the relevant span tags in the quakeInfo div
    var magDisplay = document.getElementById('mag');
    var locDisplay = document.getElementById('loc');
    var dateDisplay = document.getElementById('date');

    // JavaScript date constructor:
    // https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date
    var today = new Date();
    // Use JavaScript to get the date a week ago
    var priorDate = new Date().setDate(today.getDate() - 7);
    // Set that to an ISO8601 timestamp as required by the USGS earthquake API
    var priorDateTs = new Date(priorDate);
    var sevenDaysAgo = priorDateTs.toISOString();

    map.on('load', function() {

      map.addSource('earthquakes', {
        'type': 'geojson',
        'data': 'https://earthquake.usgs.gov/fdsnws/event/1/query?format=geojson&eventtype=earthquake&minmagnitude=1&starttime=' + sevenDaysAgo,
        'generateId': true // This ensures that all features have unique IDs
      });

      map.addLayer({
        'id': 'earthquakes-viz',
        'type': 'circle',
        'source': 'earthquakes',
        'paint': {
          // The feature-state dependent circle-radius expression will render
          // the radius size according to its magnitude when
          // a feature's hover state is set to true
          'circle-radius': [
            'case',
            ['boolean',
              ['feature-state', 'hover'],
              false
            ],
            [
              'interpolate', ['linear'],
              ['get', 'mag'],
              1, 8,
              1.5, 10,
              2, 12,
              2.5, 14,
              3, 16,
              3.5, 18,
              4.5, 20,
              6.5, 22,
              8.5, 24,
              10.5, 26
            ],
            5
          ],
          'circle-stroke-color': '#000',
          'circle-stroke-width': 1,
          // The feature-state dependent circle-color expression will render
          // the color according to its magnitude when
          // a feature's hover state is set to true
          'circle-color': [
            'case',
            ['boolean',
              ['feature-state', 'hover'],
              false
            ],
            [
              'interpolate', ['linear'],
              ['get', 'mag'],
              1, '#fff7ec',
              1.5, '#fee8c8',
              2, '#fdd49e',
              2.5, '#fdbb84',
              3, '#fc8d59',
              3.5, '#ef6548',
              4.5, '#d7301f',
              6.5, '#b30000',
              8.5, '#7f0000',
              10.5, '#000'
            ],
            '#000'
          ]
        }
      });

    });

    var quakeID = null;

    map.on('mousemove', 'earthquakes-viz', (e) => {

      map.getCanvas().style.cursor = 'pointer';
      // Set variables equal to the current feature's magnitude, location, and time
      var quakeMagnitude = e.features[0].properties.mag;
      var quakeLocation = e.features[0].properties.place;
      var quakeDate = new Date(e.features[0].properties.time);

      // Check whether features exist
      if (e.features.length > 0) {
        // Display the magnitude, location, and time in the sidebar
        magDisplay.textContent = quakeMagnitude;
        locDisplay.textContent = quakeLocation;
        dateDisplay.textContent = quakeDate;

        // If quakeID for the hovered feature is not null,
        // use removeFeatureState to reset to the default behavior
        if (quakeID) {
          map.removeFeatureState({
            source: "earthquakes",
            id: quakeID
          });
        }

        quakeID = e.features[0].id;
        
        // When the mouse moves over the earthquakes-viz layer, set the
        // feature state for the feature under the mouse
        map.setFeatureState({
          source: 'earthquakes',
          id: quakeID,
        }, {
          hover: true
        });

      }
    });

    map.on("mouseleave", "earthquakes-viz", function() {
      
      if (quakeID) {
        map.setFeatureState({
          source: 'earthquakes',
          id: quakeID
        }, {
          hover: false
        });
      }
      quakeID = null;
      // Remove the information from the previously hovered feature from the sidebar
      magDisplay.textContent = '';
      locDisplay.textContent = '';
      dateDisplay.textContent = '';
      // Reset the cursor style
      map.getCanvas().style.cursor = '';
    });
  </script>

</body>

</html>
```

## Next steps
To learn more about feature state expressions and how you can use them to dynamically style map features, explore the following resources:
- Explore the Mapbox GL JS documentation for [`setFeatureState`](https://docs.mapbox.com/mapbox-gl-js/api/#map#setfeaturestate), [`removeFeatureState`](https://docs.mapbox.com/mapbox-gl-js/api/#map#removefeaturestate), and [`getFeatureState`](https://docs.mapbox.com/mapbox-gl-js/api/#map#getfeaturestate).
- See how Mapbox used feature state to create a map using data from the 2016 presidential election in the [Live Electoral Maps: A Guide to Feature State](https://blog.mapbox.com/going-live-with-electoral-maps-a-guide-to-feature-state-b520e91a22d) blog post.
- Learn more about using events and feature state to create a per-feature styling change in the [Create a hover effect example](https://docs.mapbox.com/mapbox-gl-js/example/hover-styles/).
- Learn more about how to use Mapbox GL JS expressions in the [Get started with Mapbox GL JS expressions](/help/tutorials/mapbox-gl-js-expressions/) tutorial.
