---
title: Local search with the Geocoding API
description: This tutorial guides you through the process of creating a local search app using optional parameters from the Mapbox Geocoding API.
thumbnail: localSearchGeocodingApi
level: 2
language:
- JavaScript
prereq: Familiarity with front-end development concepts.
topics:
  - web apps
  - geocoding
prependJs:
  - "import * as constants from '../../constants';"
  - "import Note from '@mapbox/dr-ui/note';"
  - "import BookImage from '@mapbox/dr-ui/book-image';"
  - "import UserAccessToken from '../../components/user-access-token';"
contentType: tutorial
---

The Mapbox Geocoding API allows you to make forward geocodes, which means that a text query like `University of California Berkeley` gets turned into longitude and latitude coordinates. But sometimes it's not enough to find query results. Often, you want the geocoder to find query results that are biased toward a location, limited to a specific area, or both.

The Mapbox geocoder has built-in ranking that influences what results are returned, and in what order. (Read more about how search results are ranked in the [How geocoding works](/help/how-mapbox-works/geocoding/#search-result-prioritization) guide.) You can also make your Geocoding API requests even more specific by including optional query parameters.

In this tutorial, you will use the Geocoding API's `proximity` and `bbox` parameters to create a local search app for UC Berkeley that limits results to the Berkeley area and biases results around the campus itself.

<iframe width='100%' height='360px' frameBorder='0' src='/help/demos/local-search-geocoding-api/index.html'>&nbsp;</iframe>
<em class='small quiet'>View <a href='/help/demos/local-search-geocoding-api/index.html'>finished map</a>.</em>

## Getting started
To complete this tutorial, you will need:
- **A Mapbox account and access token.** Sign up for an account at [mapbox.com/signup](https://www.mapbox.com/signup/). Your access tokens are on your [Account page](https://www.mapbox.com/account).
- **Mapbox GL JS.** Mapbox GL JS is a JavaScript API for building web maps.
- **A text editor.** Use the text editor of your choice for writing HTML, CSS, and JavaScript.

## Geocoding API query structure
All Mapbox API queries must specify the API being used and the API version:
```
https://api.mapbox.com/{api_service}/{version}
```

The API service used in this tutorial is `geocoding` and the version is `v5`.
```
https://api.mapbox.com/geocoding/v5
```

Calls to the Geocoding API must also include the endpoint being used, which will either be `mapbox.places` or `mapbox.places-permanent`. (`mapbox.places-permanent` allows for permanent storage of results and for batch geocoding, and is only available to [Enterprise customers](https://www.mapbox.com/enterprise) that have a license for permanent geocodes.)

The following examples use the `mapbox.places` endpoint.

```
https://api.mapbox.com/geocoding/v5/mapbox.places
```

### Required parameters
A query to the Geocoding API must contain _search text_. The search text is either a text string for forward geocodes, or a set of coordinates for reverse geocodes. This forward geocoding example's search text is `San Francisco`:

```
https://api.mapbox.com/geocoding/v5/mapbox.places/San%20Francisco.json?access_token={{<UserAccessToken />}}
```

Regardless of whether you're performing a forward or reverse geocode, the search text needs to be followed by `.json`, since the response will be returned as a GeoJSON object.

### Optional parameters
Now comes the fun part! The Geocoding API's optional parameters allow you to customize your query so that you receive the results that are the most relevant to you. For the full list of the optional parameters that a forward geocoding request can use, see the [Geocoding API documentation](https://docs.mapbox.com/api/search/#forward-geocoding).

This tutorial will use two optional parameters that are especially useful for biasing results to a specific geographic location: `proximity` and `bbox`.


{{<Note title="View the results of an API request" imageComponent={<BookImage />}>}}
  To see the results of the example queries in the following sections, copy the API call and paste it into your browser's address bar. Add your own Mapbox access token to the end of each example. You will see the response to the API query output in GeoJSON format.
{{</Note>}}


#### The proximity parameter
The `proximity` parameter allows you to bias the response in favor of results that are closer to a specified location. This makes sure that the query results that are closer to this location are prioritized over ones that are further away. The parameter must be formatted as two comma-separated coordinates in `longitude,latitude` order. To find the coordinates of a location, you can use the [Mapbox Search Playground](https://www.mapbox.com/search-playground).

```
# Prioritizes Peets' locations in San Francisco
https://api.mapbox.com/geocoding/v5/mapbox.places/peets.json?proximity=-122.3995752,37.7881856&access_token={{<UserAccessToken />}}
```

```
# Prioritizes Peets' locations in and around Berkeley
https://api.mapbox.com/geocoding/v5/mapbox.places/peets.json?proximity=-122.2727469,37.8715926&access_token={{<UserAccessToken />}}
```

Since the `proximity` parameter is not exclusive, it does not restrict results to an area, but relevant results that are close to the provided coordinates are returned before relevant results that are further away.

#### The bbox parameter
The `bbox` parameter allows you to limit results to only those contained within a supplied bounding box. Bounding boxes need to be formatted as four coordinates separated by commas, in `minLon,minLat,maxLon,maxLat` order.

You can use any coordinates for a bounding box, as long as they describe a box shape. To find the coordinates for a bounding box, you can use the [Mapbox Search Playground](https://www.mapbox.com/search-playground).

```
# Search for Starbucks in the Washington DC area
https://api.mapbox.com/geocoding/v5/mapbox.places/starbucks.json?bbox=-77.083056,38.908611,-76.997778,38.959167&access_token={{<UserAccessToken />}}
```

The `bbox` parameter is exclusive, meaning that it will exclude any results that fall outside of the specified boundary.

### Build the Geocoding API query
Now that you have seen how to use some of the Geocoding API's optional parameters to bias results around a location and restrict results to an area, you can use them in an app. This tutorial walks you through the process of creating an app that restricts results to a set area, and then biases the results around a landmark. In this case, the set area will be Berkeley, California, and the landmark will be the UC Berkeley campus.

Using cURL, a Geocoding API query that uses `proximity` to bias results around the Berkeley campus and uses `bbox` to limit results to the Berkeley area would look like:

```
# Search text is "coffee"
# `proximity` is set to the coordinates of the campus
# `bbox` is set to encompass Berkeley CA
https://api.mapbox.com/geocoding/v5/mapbox.places/coffee.json?proximity=-122.25948,37.87221&bbox=-122.30937,37.84214,-122.23715,37.89838&access_token={{<UserAccessToken />}}
```

## Geocoding plugins and libraries
The Geocoding API's optional parameters give you powerful ways to customize your queries, but it can be unwieldy to use raw cURL API calls in your applications. The Mapbox geocoder is available through several plugins and wrapper libraries that can help you integrate it into an app:
- [Mapbox GL JS Geocoder](https://www.mapbox.com/mapbox-gl-js/plugins/#mapbox-gl-geocoder)
- [Mapbox.js Geocoder](https://www.mapbox.com/mapbox.js/api/{{constants.VERSION_MAPBOXJS}}/l-mapbox-geocoder/)
- [Mapbox Java SDK](https://www.mapbox.com/android-docs/java-sdk/examples/)
- [MapboxGeocoder.swift](https://github.com/mapbox/MapboxGeocoder.swift)
- [Mapbox JavaScript SDK](https://github.com/mapbox/mapbox-sdk-js)
- [React Geocoder](https://github.com/mapbox/react-geocoder)

This tutorial uses the Mapbox GL JS Geocoder plugin.

## Create your app
To create the local search app, you will create an HTML file and initialize the map. Then you will add the Mapbox GL JS Geocoder plugin and set the `bbox` and `proximity` parameters.

Once the app is running, you will use your browser's developer tools to see how the browser interprets the Geocoder plugin's API request.

### Set up your HTML file
Open your text editor and create a new file named `index.html`. Set up this new HTML file by pasting the following code into your text editor. This code creates the structure of the page.

There is a `<div>` element with the ID `map` in the `<body>` of the page. This `<div>` is the container in which the map will be displayed on the page.

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset='utf-8' />
  <title>Local search app</title>
  <meta name='viewport' content='initial-scale=1,maximum-scale=1,user-scalable=no' />
  <script src='https://api.mapbox.com/mapbox-gl-js/{{constants.VERSION_MAPBOXGLJS}}/mapbox-gl.js'></script>
  <link href='https://api.mapbox.com/mapbox-gl-js/{{constants.VERSION_MAPBOXGLJS}}/mapbox-gl.css' rel='stylesheet' />
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

</body>
</html>
```

### Initialize the map
Next, you will add the Mapbox GL JS code that initializes a map, which will be displayed in the `<div>` you created in the last step. In `index.html`, place the following snippet above the closing `</body>` tag. Make sure that you set the `mapbox.accessToken` variable equal to your Mapbox access token.

```html
<script>
  mapboxgl.accessToken = '{{<UserAccessToken />}}';
  var map = new mapboxgl.Map({
    container: 'map', // Container ID
    style: 'mapbox://styles/mapbox/streets-v{{constants.VERSION_STREETS_STYLE}}', // Map style to use
    center: [-122.25948, 37.87221], // Starting position [lng, lat]
    zoom: 12, // Starting zoom level
  });
</script>
```

This Mapbox GL JS code sets a style for the map, gives it coordinates on which to center, and sets a zoom level.

Save your changes. Open the HTML file in your browser to see the rendered map.

![Screenshot showing a rendered Mapbox map](/help/img/geocoding/geocoding-initial-map.png)

### Add a marker to the map
The next step is to add a marker to the map at the campus's coordinates to show the landmark's location.

After the initialization code that you wrote in the last step, add the following snippet to add a marker to the map:

```js
var marker = new mapboxgl.Marker() // initialize a new marker
  .setLngLat([-122.25948, 37.87221]) // Marker [lng, lat] coordinates
  .addTo(map); // Add the marker to the map
```

Save your changes and refresh the page in your browser. There will be a marker on the map at the specified coordinates.

### Add the geocoder
The next step is to add a geocoder using the Mapbox GL JS Geocoder plugin. To do this, first you need to add links to the geocoder's JavaScript and CSS to the head of the HTML file.

```html
<script src='https://api.mapbox.com/mapbox-gl-js/plugins/mapbox-gl-geocoder/{{constants.VERSION_GLJS_GEOCODER_PLUGIN}}/mapbox-gl-geocoder.min.js'></script>
<link rel='stylesheet' href='https://api.mapbox.com/mapbox-gl-js/plugins/mapbox-gl-geocoder/{{constants.VERSION_GLJS_GEOCODER_PLUGIN}}/mapbox-gl-geocoder.css' type='text/css' />
```

Once these links have been added, you will be able to use the Mapbox GL JS Geocoder plugin in your app. Next, add the following code above the closing `</script>` tag in your HTML file.

```js
var geocoder = new MapboxGeocoder({ // Initialize the geocoder
  accessToken: mapboxgl.accessToken, // Set the access token
  mapboxgl: mapboxgl, // Set the mapbox-gl instance
  marker: false, // Do not use the default marker style
});

// Add the geocoder to the map
map.addControl(geocoder);
```

The app you are building for this tutorial limits search results to a specific location. To give your users a visual reminder of this fact, you will use the `placeholder` parameter in the Geocoder to set custom text to display in the search bar.

Add the following line to the plugin, after the access token:
```
placeholder: 'Search for places in Berkeley'
```

Save your changes. Refresh the page in your browser, and you will see that a geocoder search box with custom text has been added to the map. When you type a search term into the box and select a result, the map flies to that location.

![Screenshot showing the Mapbox GL JS Geocoder plugin added to a map](/help/img/geocoding/geocoding-geocoder-added.png)

### Add the bbox and proximity parameters
Inside the `map.addControl` statement you added in the last step, after the `placeholder` parameter, add the `bbox` and `proximity` parameters.

In the Mapbox GL JS Geocoder plugin, the `bbox` parameter must be formatted as an _array_. The `proximity` parameter must be formatted as an _object_ with a `longitude` property and a `latitude` property. (For more information on how to format query parameters, see the [Mapbox GL JS Geocoder plugin documentation](https://github.com/mapbox/mapbox-gl-geocoder/blob/master/API.md).)

With the addition of these parameters, the entire statement will look like:

```js
var geocoder = new MapboxGeocoder({ // Initialize the geocoder
  accessToken: mapboxgl.accessToken, // Set the access token
  mapboxgl: mapboxgl, // Set the mapbox-gl instance
  marker: false, // Do not use the default marker style
  placeholder: 'Search for places in Berkeley', // Placeholder text for the search bar
  bbox: [-122.30937, 37.84214, -122.23715, 37.89838], // Boundary for Berkeley
  proximity: {
    longitude: -122.25948,
    latitude: 37.87221
  } // Coordinates of UC Berkeley
});
```

Save the HTML file and refresh the page in your browser. Now, when you enter a search into the geocoder's search box, you will not receive any results outside of the bounding box. And the results that the geocoder returns are weighted according to their proximity to the Berkeley campus.

### Place markers at selected results

{{<Note title="Adding a custom marker style" imageComponent={<BookImage />}>}}
  The Mapbox GL Geocoder sets a marker at the search result location by default. This example adds a custom marker as a new layer instead. If you want to use the default marker provided by the geocoder, remove the line `marker: false,` from the new geocoder instantiation.
{{</Note>}}

The final step for creating this app is to place a custom marker on the map at the location of a selected search result. The logic for doing this needs to be wrapped in a [`map.on('load')` event](https://www.mapbox.com/mapbox-gl-js/api/#map#on) so that it is not triggered before the map itself has been loaded. Before the closing `</script>` tag, paste the following JavaScript:

```js
// After the map style has loaded on the page,
// add a source layer and default styling for a single point
map.on('load', function() {
  map.addSource('single-point', {
    type: 'geojson',
    data: {
      type: 'FeatureCollection',
      features: []
    }
  });

  map.addLayer({
    id: 'point',
    source: 'single-point',
    type: 'circle',
    paint: {
      'circle-radius': 10,
      'circle-color': '#448ee4'
    }
  });

  // Listen for the `result` event from the Geocoder
  // `result` event is triggered when a user makes a selection
  //  Add a marker at the result's coordinates
  geocoder.on('result', function(e) {
    map.getSource('single-point').setData(e.result.geometry);
  });
});
```

Save the HTML file and refresh the page in your browser. When search and select a result, a marker will be placed at the result's coordinates.

### View the API call in developer tools
To see what's going on behind the scenes when you use the Mapbox GL JS Geocoder plugin,  you can view the raw API call using your browser's developer tools. This can be useful for debugging a query if the returned results are not what you expect.

{{<Note title="How do I open developer tools?" imageComponent={<BookImage />}>}}
  The following instructions are for Chrome's developer tools layout. For other browsers, some details may vary but in general the workflow will be similar. Read your browser's help page for details on how to open the developer tools and find the network information.
{{</Note>}}

1. Load the page you created in this tutorial in your browser, or refresh it if it's already open.
1. Open the browser's developer tools. (In Chrome, you can do this by typing `command + option + i` or `command + option + j`.)
1. Type a text phrase into the app's geocoder search bar and select a result. (The example below is for the search term "coffee".)
1. Click on the **Network** tab.
1. In the _Filter_ search bar, type in "geocoding". This will narrow the list of network calls down to those made by the Mapbox Geocoding API.
1. You will likely see more than one Geocoding API call in the list, each representing a different stage of the search text. Click on the option that has the complete search text (for example, "coffee" instead of "coff").
1. In the Request URL section, you will see a request that is like the cURL API request that you created in the [Build the Geocoding API query](#build-the-geocoding-api-query) section of this tutorial:

```
https://api.mapbox.com/geocoding/v5/mapbox.places/coffee.json?access_token={{<UserAccessToken />}}&proximity=-122.259%2C37.872&bbox=-122.30937%2C37.84214%2C-122.23715%2C37.89838&limit=5
```

The difference between the query returned by the browser and the one you created earlier is that this one also includes the `limit` parameter, with the default value of `5` passed in.

## Finished product
You have completed a local search app that, when a user enters a query into the geocoder search box, biases the results around the UC Berkeley campus and excludes any results that are located outside the Berkeley area.

<iframe width='100%' height='360px' frameBorder='0' src='/help/demos/local-search-geocoding-api/index.html'>&nbsp;</iframe>
<em class='small quiet'>View <a href='/help/demos/local-search-geocoding-api/index.html'>finished map</a>.</em>

The final HTML file will look like the following:

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset='utf-8' />
    <title>Local search app</title>
    <meta name='viewport' content='initial-scale=1,maximum-scale=1,user-scalable=no' />
    <script src='https://api.mapbox.com/mapbox-gl-js/{{constants.VERSION_MAPBOXGLJS}}/mapbox-gl.js'></script>
    <link href='https://api.mapbox.com/mapbox-gl-js/{{constants.VERSION_MAPBOXGLJS}}/mapbox-gl.css' rel='stylesheet' />
    <script src='https://api.mapbox.com/mapbox-gl-js/plugins/mapbox-gl-geocoder/{{constants.VERSION_GLJS_GEOCODER_PLUGIN}}/mapbox-gl-geocoder.min.js'></script>
    <link rel='stylesheet' href='https://api.mapbox.com/mapbox-gl-js/plugins/mapbox-gl-geocoder/{{constants.VERSION_GLJS_GEOCODER_PLUGIN}}/mapbox-gl-geocoder.css' type='text/css' />
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
  mapboxgl.accessToken = '{{<UserAccessToken />}}';
  var map = new mapboxgl.Map({
    container: 'map', // Container ID
    style: 'mapbox://styles/mapbox/streets-v{{constants.VERSION_STREETS_STYLE}}', // Map style to use
    center: [-122.25948, 37.87221], // Starting position [lng, lat]
    zoom: 12, // Starting zoom level
  });

  var marker = new mapboxgl.Marker() // Initialize a new marker
    .setLngLat([-122.25948, 37.87221]) // Marker [lng, lat] coordinates
    .addTo(map); // Add the marker to the map

  var geocoder = new MapboxGeocoder({ // Initialize the geocoder
    accessToken: mapboxgl.accessToken, // Set the access token
    mapboxgl: mapboxgl, // Set the mapbox-gl instance
    marker: false, // Do not use the default marker style
    placeholder: 'Search for places in Berkeley', // Placeholder text for the search bar
    bbox: [-122.30937, 37.84214, -122.23715, 37.89838], // Boundary for Berkeley
    proximity: {
      longitude: -122.25948,
      latitude: 37.87221
    } // Coordinates of UC Berkeley
  });

  // Add the geocoder to the map
  map.addControl(geocoder);

  // After the map style has loaded on the page,
  // add a source layer and default styling for a single point
  map.on('load', function() {
    map.addSource('single-point', {
      type: 'geojson',
      data: {
        type: 'FeatureCollection',
        features: []
      }
    });

    map.addLayer({
      id: 'point',
      source: 'single-point',
      type: 'circle',
      paint: {
        'circle-radius': 10,
        'circle-color': '#448ee4'
      }
    });

    // Listen for the `result` event from the Geocoder
    // `result` event is triggered when a user makes a selection
    // Add a marker at the result's coordinates
    geocoder.on('result', function(ev) {
      map.getSource('single-point').setData(ev.result.geometry);
    });
  });
</script>
</body>
</html>
```

## Next steps
There are a lot of things you could do to build this app out more. You could:

- Use Turf.js to analyze the distances of the various results from the UC Berkeley campus. (See the [Sort stores by distance](/help/tutorials/geocode-and-sort-stores/) tutorial.)
- Experiment with the Mapbox GL JS Geocoder plugin's `filter` function to get even more granular results. (See the [Limit geocoder results to a named region](https://www.mapbox.com/mapbox-gl-js/example/mapbox-gl-geocoder-limit-region/) example.)
