---
title: "Add points to a web map, part 3: add interactivity"
description: Add popups when markers are clicked using Mapbox GL JS.
thumbnail: addPointsToAMap
level: 1
topics:
- web apps
language:
- JavaScript
prependJs:
  - "import * as constants from '../../constants';"
  - "import UserAccessToken from '../../components/user-access-token';"
  - "import DemoIframe from '@mapbox/dr-ui/demo-iframe';"
contentType: tutorial
---

This is the third and final part in a [tutorial series](https://www.mapbox.com/studio-manual/help/#add-points-to-a-map) that teaches you how to add points to a map using the Mapbox Studio dataset editor, the Mapbox Studio style editor, and Mapbox GL JS.

*Part 3* focuses on using **Mapbox GL JS**, a JavaScript library, and will require you to write code. In this tutorial, you will learn how to:

- Add a custom style to a Mapbox GL JS map
- Add popups when a [marker](/help/glossary/marker/) is clicked

{{
  <DemoIframe src="/help/demos/add-points-to-a-map/index.html" />
}}

## Getting started

There are a few resources you will need to follow along with this guide:

- **The "Chicago Parks" custom style**. You will need a [style](/help/glossary/style) containing markers for 10 Chicago parks. You can learn how to create this style in [Add points to a web map, part 1: create a dataset](/help/tutorials/add-points-pt-1) and [Add points to a web map, part 2: create a style](/help/tutorials/add-points-pt-2).
- **Development environment**. This guide requires writing code. See _Get ready to write code_ below for tips on how to get started.

### Get ready to write code

To create an interactive map with popups you will need to use [Mapbox GL JS](https://www.mapbox.com/mapbox-gl-js/api/). This will require writing  code. First, you will need to get setup with a development environment to write HTML, CSS, and JavaScript. If you are new to writing code, you may want to explore a resource like [Codecademy](https://www.codecademy.com/) to learn more about how front-end development works before using Mapbox GL JS. Here's what you'll need to do:

- Download a text editor (for example, [Sublime Text](https://www.sublimetext.com/) or [Atom](https://atom.io/)).
- Familiarize yourself with JavaScript and front-end development concepts.

## Create an HTML file

Create a new HTML file in your text editor to initialize a Mapbox GL JS map.

### Initialize your map

1. Open your text editor.
1. Copy and paste the code below into your text editor to initialize your Mapbox GL JS map.
1. Make sure `mapboxgl.accessToken` is set equal to your access token.
    - You can find your access token on your [Access tokens page](https://www.mapbox.com/account/access-tokens/) when you sign into your [Mapbox Account](https://www.mapbox.com/account).
1. Replace `your-style-URL-here` with your own style URL. [Need help finding your style URL?](/help/glossary/style-url/)
1. Save your file as "index.html."
1. Open the file in a browser.
1. You should see a map displaying your data in the browser window.

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset='utf-8' />
    <title>Points on a map</title>
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
    mapboxgl.accessToken = '{{ <UserAccessToken /> }}'; // replace this with your access token
    var map = new mapboxgl.Map({
      container: 'map',
      style: 'your-style-URL-here', // replace this with your style URL
      center: [-87.661557, 41.893748],
      zoom: 10.7
    });
    // code from the next step will go here
    </script>
  </body>
</html>
```

## Add popups

After you have successfully displayed your map, you will need to add a little more code to allow the user to interact with your markers. This code will include:
  - [`queryRenderedFeatures`](https://www.mapbox.com/mapbox-gl-js/api/#map#queryrenderedfeatures): This Mapbox GL JS method will generate a list of all the points on your map and the feature properties associated with each.
  - [`mapboxgl.Popup`](https://www.mapbox.com/mapbox-gl-js/api/#popup): This method is used to create popups that show certain feature properties. The `Popup` component has several different instance members that you can use to customize the popup elements. In this example, you will use:
      - **`Popup.setLngLat()`:** Sets the geographical location of the popup's anchor.
      - **`Popup.setHTML()`:** Sets the popup's content to the HTML provided as a string. The specified properties must match the name of the properties you would like to display in your popups. In the code below, the properties that will display are the `title` and `description` properties for each feature.
      - **`Popup.addTo(map)`:** Adds the popup to a map.
  - An event listener: This event listener will make sure that popups are only shown when the user clicks a marker.

### Add more code

1. Copy and paste the code below into your HTML file after the code that initializes your map, but before the `</script>` tag.
1. In the variable `features`, make sure you replace `layer-name-here` with the name of your layer as seen in the style editor. This is probably `chicago-parks` if you have been following the earlier tutorials in this series.
1. Refresh your browser page. You will be able to click on the markers and see titles and descriptions displayed in the popups.

```js
map.on('click', function(e) {
  var features = map.queryRenderedFeatures(e.point, {
    layers: ['layer-name-here'] // replace this with the name of the layer
  });

  if (!features.length) {
    return;
  }

  var feature = features[0];

  var popup = new mapboxgl.Popup({ offset: [0, -15] })
    .setLngLat(feature.geometry.coordinates)
    .setHTML('<h3>' + feature.properties.title + '</h3><p>' + feature.properties.description + '</p>')
    .addTo(map);
});
```

## Final product

You've made a map using the Mapbox Studio dataset editor, Mapbox Studio style editor, and Mapbox GL JS that incorporates custom data and styles and allows for user interaction.

{{
  <DemoIframe src="/help/demos/add-points-to-a-map/index.html" />
}}

## Next steps

To learn about more things you can do with Mapbox Studio, explore the [Mapbox Studio manual](https://www.mapbox.com/studio-manual/). For more information on Mapbox GL JS and how it works, read our guide on how [Mapbox web applications work](/help/how-mapbox-works/web-apps/).
