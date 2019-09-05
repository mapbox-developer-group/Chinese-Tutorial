---
title: Get started with Mapbox GL JS expressions
description: Learn how to write expressions in Mapbox GL JS.
thumbnail: glJsExpressions
level: 2
prereq: Familiarity with front-end development concepts.
topics:
- web apps
- map design
language:
- JavaScript
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

In this guide you'll learn how to write expressions in Mapbox GL JS to style custom data based on a data property and by zoom level.

{{
  <DemoIframe src="/help/demos/intro-to-expressions/step-four.html" />
}}

## Getting started

- **A Mapbox account and access token**. Sign up for an account at [mapbox.com/signup](https://www.mapbox.com/signup/). You can find your [access tokens](/help/how-mapbox-works/access-tokens/) on your [Account page](https://www.mapbox.com/account/).
- **Mapbox GL JS**. You'll be using, Mapbox GL JS, our JavaScript library.
- **A style URL**. You'll need a [style URL](/help/glossary/style-url/) to initialize your map. You'll walk through how to find your style URL in the _Add a designer style to your account_ section of this guide.
- **Data**. In this tutorial, you'll be using a CSV file of [HPC Landmarks from Open Minneapolis](http://opendata.minneapolismn.gov/datasets/hpc-landmarks/data).

{{
<Button href="/help/demos/intro-to-expressions/HPC_landmarks.csv" passthroughProps={{ download: "HPC_landmarks" }} >
    <Icon name='arrow-down' inline={true} /> Download the data
</Button>
}}

## What are expressions?

In the Mapbox Style Specification, the value for any layout property, paint property, or filter may be specified as an expression. Expressions define how one or more feature property value and/or the current zoom level are combined using logical, mathematical, string, or color operations to produce the appropriate style property value or filter decision.

A **property expression** is any expression defined using a reference to feature property data. Property expressions allow the appearance of a feature to change with its properties. They can be used to visually differentiate types of features within the same layer or create data visualizations.

{{
  <Note title='Property expressions vs. property functions' imageComponent={<BookImage />}>
    <p>If you have worked with Mapbox GL JS before, you may be familiar with property <em>functions</em>. Property <em>expressions</em> can help you achieve similar effects as property <em>functions</em>, with much more flexibility and functionality. Property expressions were introduced in <a href='https://github.com/mapbox/mapbox-gl-js/blob/master/CHANGELOG.md#0410-october-11-2017'>Mapbox GL JS v0.41.0</a>. <strong>While property functions are available, they will ultimately be deprecated and replaced by property expressions.</strong></p>
  </Note>
}}

### Uses

There are countless ways to apply property expressions to your application, including:

- **Data-driven styling**: Specify style rules based on one or more data attribute.
- **Arithmetic**: Do arithmetic on source data, for example performing calculations to convert units.
- **Conditional logic**: Use if-then logic, for example to decide exactly what text to display for a label based on which properties are available in the feature or even the length of the name.
- **String manipulation**: Take control over label text with things like uppercase, lowercase, and title case transforms without having to edit, re-prepare and re-upload your data.

### Syntax

Mapbox GL JS expressions uses a Lisp-like syntax, represented using JSON arrays. Expressions follow this format:

```
[expression_name, argument_0, argument_1, ...]
```

The `expression_name` is the **expression operator**, for example, you would use [`'*'`](https://www.mapbox.com/mapbox-gl-js/style-spec/#expressions-*) to multiply two arguments or [`'case'`](https://www.mapbox.com/mapbox-gl-js/style-spec/#expressions-case) to create conditional logic. For a complete list of all available expressions see the [Mapbox Style Specification](https://www.mapbox.com/mapbox-gl-js/style-spec/#expressions).

The **arguments** are either _literal_ (numbers, strings, or boolean values) or else themselves expressions. The number of arguments varies based on the expression.

Here's one example using an expression to calculate an arithmetic expression (π * 3<sup>2</sup>):

```
['*', ['pi'], ['^', 3, 2]]
```

This example uses a [`'*'`](https://www.mapbox.com/mapbox-gl-js/style-spec/#expressions-*) expression to multiply two arguments. The first argument is [`'pi'`](https://www.mapbox.com/mapbox-gl-js/style-spec/#expressions-pi), which is an expression that returns the mathematical constant pi. The second arguement is another expression: a [`'^'`](https://www.mapbox.com/mapbox-gl-js/style-spec/#expressions-^) expression with two arguments of its own. It will return 3<sup>2</sup>, and the result will be multiplied by π.

## Set up a map

Now that you've had an introduction to the uses and syntax for expressions, it's time to test it out yourself! Initialize a map with Mapbox GL JS and add the custom data as a circle layer.

### Add a designer style to your account

The map in this guide uses one of our designer styles. To use a designer style you'll need to start by adding it to your account. Sign into your Mapbox account and visit the designer map page to add a new style to your account:

1. Visit [mapbox.com/designer-maps](https://www.mapbox.com/designer-maps/).
1. Find the _North Star_ style and click **Add this style**.
1. The style will automatically be added to your Mapbox account.

When the style is added to your account, it will appear on the Styles page in Mapbox Studio. From here, you can find the [style URL](/help/glossary/style-url) for the style. You'll use the style URL to add this style to your map:

1. Find the style on your [Styles page](https://www.mapbox.com/studio/styles).
1. Click on the **Menu {{<Icon name='menu' inline={true} />}}** next to the style name.
1. Find the _Style URL_. You can use the {{<Icon name='clipboard' inline={true} />}} clipboard icon to copy the style URL, which you'll use in the _Initialize a map with data_ section.

### Upload data

In this guide, you'll use a [vector tileset](/help/glossary/tileset) to display data in your application. You can create a vector tileset by uploading the CSV you downloaded earlier to Mapbox Studio:

1. Visit the [Tilesets page](https://www.mapbox.com/studio/tilesets) in Mapbox Studio.
1. Click **New tileset**.
1. Select the CSV you downloaded at the beginning of this tutorial and click **Confirm**.
1. A popover will appear in the bottom right showing the progress of your upload.
1. Once the upload has _Succeeded_, the tileset will be ready to use! Click on the name of the tileset in the popover, which will open the tileset information page.
1. Take note of the *tileset ID* on the right side of the tileset information page. You will use the ID to add this tileset to your map in the next step.

### Initialize a map with data

In a text editor, create a new `index.html` file and use the following code to initialize your map. You will need to:

1. Make sure `mapboxgl.accessToken` is set equal to one of your [access tokens](/help/glossary/access-token/).
1. Replace `your-style-url-here` with your [style URL](/help/glossary/style-url/).
1. Replace `your-tileset-id-here` with the [tileset ID](/help/glossary/tileset-id) for the tileset you created.
1. Replace `your-source-layer-here` with the name of the [source layer](/help/glossary/source-layer/) in your tileset.

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset='utf-8' />
    <title></title>
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
    container: 'map', // container id
    style: 'your-style-url-here', // stylesheet location
    center: [-93.261, 44.971], // starting position [lng, lat]
    zoom: 10 // starting zoom
  });

  map.on('load', function() {
    map.addLayer({
      id: 'historical-places',
      type: 'circle',
      source: {
        type: 'vector',
        url: 'mapbox://your-tileset-id-here'
      },
      'source-layer': 'your-source-layer-here',
    });
  });

  </script>

  </body>
</html>
```

Run your application in a browser, and you will see a light colored map centered on Minneapolis with black dots scattered across the city.

{{
  <DemoIframe src="/help/demos/intro-to-expressions/step-one.html" />
}}

## Write a property expression

Next, you'll write an expression to style the radius of each circle based on the age of each historic landmark. In this data file, provided by the City of Minneapolis's open data portal, the age of the historic landmark is not provided, but the year of construction is provided. You can use arithmetic to calculate the age based on the current year and style the `circle-radius` paint property based on the age.

### Calculate the age of each landmark

Start by calculating the age of the landmark. Here's the expression you'll use:

```
['-', 2017, ['number', ['get', 'Constructi'], 2017]]
```

Use a `'-'` expression with two arguments. The first argument is a number (the current year, `2017`). The second argument is another expression (a `'number'` expression) with two arguments. This expression will convert the first argument to a number. If the first argument doesn't have a value, then the second argument, the current year `2017`, will be used.

The first argument for the `'number'` expression is yet another expression &mdash; this time a `'get'` expression that retrieves the object property value of its only argument, `'Constructi'`. (`'Constructi'` is the `'Construction_Date'` from the original CSV file, but the name of the field was shortened in the upload process.) The value that is retrieved using `'get'` is turned into a `'number'`.

Ultimately, this expression results in the age of the landmark, essentially `2017 - year of construction`.

### Specify the circle radius

Use this expression inside the existing `addLayer` function in your code:

```js
map.on('load', function() {
  map.addLayer({
    id: 'historical-places',
    type: 'circle',
    source: {
      type: 'vector',
      url: 'mapbox://your-tileset-id-here'
    },
    'source-layer': 'your-source-layer-here',
    paint: {
      'circle-radius': ['-', 2017, ['number', ['get', 'Constructi'], 2017]],
      'circle-opacity': 0.8,
      'circle-color': 'rgb(171, 72, 33)'
    }
  });
});
```

<!-- copyeditor ignore built-->
Refresh your browser and you'll see that the circle radius has changed dramatically. With the current expression, the radius of a circle representing a landmark that was built in 1950 would be 67 pixels. Next, you'll adjust the radius to be more appropriate in this context.

{{
  <DemoIframe src="/help/demos/intro-to-expressions/step-two.html" />
}}

### Adjust the circle radius

Wrap the expression in one other expression to make the size of the circles look better in this context. In this case, you'll divide the age of the landmark by `10`.

```js
map.on('load', function() {
  map.addLayer({
    id: 'historical-places',
    type: 'circle',
    source: {
      type: 'vector',
      url: 'mapbox://your-tileset-id-here'
    },
    'source-layer': 'your-source-layer-here',
    paint: {
      'circle-radius': [
        '/',
        ['-', 2017, ['number', ['get', 'Constructi'], 2017]],
        10
      ],
      'circle-opacity': 0.8,
      'circle-color': 'rgb(171, 72, 33)'
    }
  });
});
```

Refresh your browser and you'll see an updated map.

{{
  <DemoIframe src="/help/demos/intro-to-expressions/step-three.html" />
}}

## Add a zoom expression

The circles are still overlapping quite a bit at the starting zoom level, `10.5`, but they look good at higher zoom levels. You can use a zoom expression to address this issue. A **zoom expression** is any expression defined using `['zoom']`. Such expressions allow the appearance of a layer to change with the map’s zoom level. Zoom expressions can be used to create the illusion of depth and control data density.

Use an [`'interpolate'`](https://www.mapbox.com/mapbox-gl-js/style-spec/#expressions-interpolate) expression. An `'interpolate'` expression produces continuous, smooth results by interpolating between pairs of input and output values ("stops"). In this case, use `['linear']` to interpolate linearly between a pair of stops slightly less than and slightly greater than the input. Then, specify that the radius should be the `age of the landmark / 30` at zoom level `10` and `age of the landmark / 10` at zoom level `13`.

```js
map.on('load', function() {
  map.addLayer({
    id: 'historical-places',
    type: 'circle',
    source: {
      type: 'vector',
      url: 'mapbox://your-tileset-id-here'
    },
    'source-layer': 'your-source-layer-here',
    paint: {
      'circle-radius': [
        'interpolate', ['linear'], ['zoom'],
        10, ['/', ['-', 2017, ['number', ['get', 'Constructi'], 2017]], 30],
        13, ['/', ['-', 2017, ['number', ['get', 'Constructi'], 2017]], 10],
      ],
      'circle-opacity': 0.8,
      'circle-color': 'rgb(171, 72, 33)'
    }
  });
});
```

{{
  <Note imageComponent={<BookImage />}>
    <p>If you've worked with <a href='https://www.mapbox.com/mapbox-gl-js/style-spec/#types-function'>property <em>functions</em></a> before, notice that <code>interpolate</code> expressions allow you to achieve the same effect as stop functions.</p>
  </Note>
}}

Refresh your browser and zoom into the map to see the resulting effect.

{{<img src='/help/img/gl-js/expressions-step-four.gif' alt='animated screenshot zooming in and out and panning around a map with custom data styled using expressions' className='mx-auto block' />}}

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset='utf-8' />
    <title>Minneapolis Landmarks</title>
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
      container: 'map', // container id
      style: 'your-style-url-here', // stylesheet location
      center: [-93.261, 44.971], // starting position [lng, lat]
      zoom: 10.5 // starting zoom
    });

    map.on('load', function() {
      map.addLayer({
        id: 'historical-places',
        type: 'circle',
        source: {
          type: 'vector',
          url: 'mapbox://your-tileset-id-here'
        },
        'source-layer': 'your-source-layer-here',
        paint: {
          'circle-radius': [
            'interpolate', ['linear'], ['zoom'],
            10, ['/', ['-', 2017, ['number', ['get', 'Constructi'], 2017]], 30],
            13, ['/', ['-', 2017, ['number', ['get', 'Constructi'], 2017]], 10],
          ],
          'circle-opacity': 0.8,
          'circle-color': 'rgb(171, 72, 33)'
        }
      });
    });
  </script>
  </body>
</html>
```

## Final product

You've styled custom data using expressions in Mapbox GL JS!

{{
  <DemoIframe src="/help/demos/intro-to-expressions/step-four.html" />
}}

## Next steps

There are many other ways you can use expressions in Mapbox GL JS. For more information:

- Read about expressions in the [Mapbox Style Specification](https://www.mapbox.com/mapbox-gl-js/style-spec/#expressions).
- Explore other [Mapbox GL JS examples](https://www.mapbox.com/mapbox-gl-js/example/simple-map/) that use expressions:
  - [Create and style clusters](https://www.mapbox.com/mapbox-gl-js/example/cluster/)
  - [Create a hover effect](https://www.mapbox.com/mapbox-gl-js/example/hover-styles/)
  - [Create a time slider](https://www.mapbox.com/mapbox-gl-js/example/timeline-animation/)
  - [Filter features within map view](https://www.mapbox.com/mapbox-gl-js/example/filter-features-within-map-view/)
  - [Update a choropleth layer by zoom level](https://www.mapbox.com/mapbox-gl-js/example/updating-choropleth/)
