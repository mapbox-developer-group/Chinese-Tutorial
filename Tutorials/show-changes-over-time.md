---
title: Show changes over time with Mapbox GL JS
description: Build a map application with Mapbox GL JS to visualize changes in data over time.
thumbnail: showDataChangeOverTime
level: 3
topics:
- web apps
language:
- JavaScript
prereq: Familiarity with front-end development concepts. Some advanced JavaScript required.
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

{{
  <Note
    imageComponent={<BookImage />}
    title='Property functions vs. property expressions'
  >
    <p>This tutorial uses property <em>expressions</em>. This new feature was introduced in <a href='https://github.com/mapbox/mapbox-gl-js/blob/master/CHANGELOG.md#0410-october-11-2017'>Mapbox GL JS v0.41.0</a>. Property <em>expressions</em> can help you achieve similar effects as property <em>functions</em>, but with much more flexibility and functionality. <strong>While <a href='https://www.mapbox.com/mapbox-gl-js/style-spec#other-function'>property functions</a> are available, they will ultimately be deprecated and replaced by property expressions.</strong></p>
    <p>Read more about property expressions in the <a href='https://www.mapbox.com/mapbox-gl-js/style-spec/#expressions'>Mapbox Style Specification</a> and in the <a href='/help/tutorials/mapbox-gl-js-expressions/'>Get started with Mapbox GL JS expressions</a> guide.</p>
  </Note>
}}

This tutorial will show how to build a map that shows data change over time using [Mapbox GL JS](https://www.mapbox.com/mapbox-gl-js/). The source data you'll be working with in this guide is from [NYC OpenData](https://data.cityofnewyork.us/) and contains more than 15,000 motor vehicle collisions in New York City that occurred in January 2016.

If you're new to Mapbox GL JS you might want to read [Mapbox GL JS fundamentals](/help/how-mapbox-works/web-apps/) first.

{{
  <DemoIframe src="/help/demos/show-changes-over-time/step-final.html" />
}}

## Get started

There are a few resources you'll need before getting started:

- [**An access token**](/help/glossary/access-token/) from your Mapbox account. The access token is used to associate a map with your account and you can find it on your [Account page](https://www.mapbox.com/account).
- **Data**. This GeoJSON file contains 15,273 geocoded motor vehicle collision incidents from January 2016, pulled from [NYC OpenData](https://data.cityofnewyork.us/Public-Safety/NYPD-Motor-Vehicle-Collisions/h9gi-nx95).
{{
<Button href="/help/data/collisions1601.geojson" passthroughProps={{ download: "collisions1601.geojson" }}>
    <Icon name='arrow-down' inline={true} /> Download data
</Button>
}}
- **A text editor** for writing HTML, CSS, and JavaScript.

## Add a map

Before you start adding your NYC collision data, you need to create a map to put it on. Start by creating an HTML file and then initialize the map object on the page. This guide will require several files, so we recommend creating a project folder on your computer to keep them together.

### Create an HTML file

In your project folder, create an `index.html` file. Set up the document by adding Mapbox GL JS and CSS to your `head`.

```html
<meta charset='utf-8' />
<title>NYC motor vehicle collisions</title>
<meta name='viewport' content='initial-scale=1,maximum-scale=1,user-scalable=no' />
<script src='https://api.mapbox.com/mapbox-gl-js/{{constants.VERSION_MAPBOXGLJS}}/mapbox-gl.js'></script>
<link href='https://api.mapbox.com/mapbox-gl-js/{{constants.VERSION_MAPBOXGLJS}}/mapbox-gl.css' rel='stylesheet' />
```

Next, create a map container and a container for your legend and data interactivity elements in `body`.

```html
<div id='map'></div>
<div id='console'>
  <h1>Motor vehicle collisions</h1>
  <p>Data: <a href='https://data.cityofnewyork.us/Public-Safety/NYPD-Motor-Vehicle-Collisions/h9gi-nx95'>Motor vehicle collision injuries and deaths</a> in NYC, Jan 2016</p>
</div>
```

Apply some CSS to create the page layout. Create a pair of `style` tags at the end of your `head`, then add:

```css
body {
  margin: 0;
  padding: 0;
  font-family: 'Helvetica Neue', Helvetica, Arial, Sans-serif;
}

#map {
  position: absolute;
  top: 0;
  bottom: 0;
  width: 100%;
}

h1 {
  font-size: 20px;
  line-height: 30px;
}

h2 {
  font-size: 14px;
  line-height: 20px;
  margin-bottom: 10px;
}

a {
  text-decoration: none;
  color: #2dc4b2;
}

#console {
  position: absolute;
  width: 240px;
  margin: 10px;
  padding: 10px 20px;
  background-color: white;
}
```

### Initialize the map

Once you have the structure done, you can initialize the map with Mapbox GL JS. Insert a pair of `script` tags at the end of `body` &mdash; you will write all the following code (JavaScript) between these tags.

Start by creating a new `map` object using `new mapboxgl.Map()` and store it in a variable called `map`.

```js
mapboxgl.accessToken = '{{ <UserAccessToken /> }}';

var map = new mapboxgl.Map({
  container: 'map', // container element id
  style: 'mapbox://styles/mapbox/light-v{{constants.VERSION_LIGHT_STYLE}}',
  center: [-74.0059, 40.7128], // initial map center in [lon, lat]
  zoom: 12
});
```

If you load the page, it should look like this:

{{
  <DemoIframe src="/help/demos/show-changes-over-time/step-one.html" />
}}

## Load your data

Once you get the page structure and map done and onto the page, it's time to load in your data, get it styled, and add a legend. Fortunately, Mapbox GL JS has some handy functions that can help! First, make sure that the `collisions1601.geojson` file you downloaded is in your project folder.

### Add a layer

To add data to your map using Mapbox GL JS, you will need to add a [layer](/help/glossary/layer) that includes a [source](/help/glossary/source). In this example, you will use the GeoJSON file you downloaded above as your source.

{{
  <Note
    imageComponent={<BookImage />}
  >
    <p>Be sure to save and store the GeoJSON file in the same domain as your project. You will also need to run this application from a local web server, otherwise you will receive a <a href='http://en.wikipedia.org/wiki/Cross-origin_resource_sharing'>Cross-origin Resource Sharing (CORS)</a> error. <a href='http://www.2ality.com/2014/06/simple-http-server.html'>Python's SimpleHTTPServer</a> is included on many computers and is a good choice if this is your first time running a local server.</p>
  </Note>
}}

In this example, you'll use [expressions](https://www.mapbox.com/mapbox-gl-js/style-spec#expressions) to set the style of the points based on a property in the data. This kind of [data-driven styling](/help/glossary/data-driven-styling) allows you to add an extra dimension to you map visualization, helping convey a particular insight or message to your readers. In this case, you can make the map more informative by applying styles based on the `Casualty` property in the data, which is the total number of people injured or killed in the collision. The code below changes both the size and color of the points based on the `Casualty` field.

Both of the expressions used below are [`'interpolate'`](https://www.mapbox.com/mapbox-gl-js/style-spec#expressions-interpolate) expressions. This kind of expression interpolates continuously between pairs of input and output values. In this instance, 'linear' interpolation can be used for  `circle-radius` and `circle-color` to make sure that interpolation occurs smoothly and linearly between the pairs of stops.

Also, note the `map.on('load', function(){})` code below &mdash; this tells your browser to wait until the map is finished loading before trying to add new things to it. Any code that adds layers should be inside of this callback function.


```js
map.on('load', function() {
  map.addLayer({
    id: 'collisions',
    type: 'circle',
    source: {
      type: 'geojson',
      data: './collisions1601.geojson' // replace this with the url of your own geojson
    },
    paint: {
      'circle-radius': [
        'interpolate',
        ['linear'],
        ['number', ['get', 'Casualty']],
        0, 4,
        5, 24
      ],
      'circle-color': [
        'interpolate',
        ['linear'],
        ['number', ['get', 'Casualty']],
        0, '#2DC4B2',
        1, '#3BB3C3',
        2, '#669EC4',
        3, '#8B88B6',
        4, '#A2719B',
        5, '#AA5E79'
      ],
      'circle-opacity': 0.8
    }
  });
});

```

### Create a legend

To describe the data you added, create a legend to communicate what each color and size means. Begin by creating a new `div`  with class `session` inside the `console` `div` you added earlier.

```html
<div class='session'>
  <h2>Casualty</h2>
  <div class='row colors'>
  </div>
  <div class='row labels'>
    <div class='label'>0</div>
    <div class='label'>1</div>
    <div class='label'>2</div>
    <div class='label'>3</div>
    <div class='label'>4</div>
    <div class='label'>5+</div>
  </div>
</div>
```

Next, apply some CSS to define how the new `session` class should be styled. Create a color gradient using the same colors as the stops of the `circle-color` values you defined in your layer. This should go inside the `style` tags you added earlier.

```css
.session {
  margin-bottom: 20px;
}

.row {
  height: 12px;
  width: 100%;
}

.colors {
  background: linear-gradient(to right, #2dc4b2, #3bb3c3, #669ec4, #8b88b6, #a2719b, #aa5e79);
  margin-bottom: 5px;
}

.label {
  width: 15%;
  display: inline-block;
  text-align: center;
}
```

After adding the CSS and refreshing your browser, you should see the following:

{{
  <DemoIframe src="/help/demos/show-changes-over-time/step-two.html" />
}}

## Add a time slider

With the data symbolized by casualty, your map is already telling a compelling story. To make it more compelling, you can add a time slider to allow your readers to filter the collision data by time of day.

### Add a map filter

Besides providing the value of a paint or layout property, you can use expressions as filters. By adding a [`==`](https://www.mapbox.com/mapbox-gl-js/style-spec#expressions-==) expression as a [filter](https://www.mapbox.com/mapbox-gl-style-spec/#types-filter) with the structure `"filter": ['==', ['type',['get', 'key']],'value']`, you can single out all features where the 'key' is equal to the 'value' of the specified type. Add the following code to the end of the `addLayer()` options you wrote earlier:

```
filter: ['==', ['number', ['get', 'Hour']], 12]
```

Refresh the map. You should see a lot fewer collisions!

### Create a slider bar

You don't only want to show collisions that happened at noon, though &mdash; you want the user to be able to control what hour of the day the map shows. To do this, you can add a time slider in the `console` div by adding a new `session` div after `legend`. There are 24 hours in a day labeled by the integers 0-23 in the dataset, so you'll set the input's `min` and `max` attributes to `0` and `23`, respectively, and the initial value to 12, or 12PM. Add the following code below the other `session` div you added in a previous step:

```html
<div class='session' id='sliderbar'>
  <h2>Hour: <label id='active-hour'>12PM</label></h2>
  <input id='slider' class='row' type='range' min='0' max='23' step='1' value='12' />
</div>
```

### Add interactivity

Now, add some code to connect the slider with the map. Begin by adding an event listener to the slider called `onInput`, which listens for any change in the slider's value. Next, use Mapbox GL JS's `setFilter(layer, filter)` method to change your layer's `filter` property whenever the `input` event fires. Finally, add a bit of math to add `PM` or `AM` to the time displayed next to your slider.

Add this right after `addLayer()` in your script:

```js
document.getElementById('slider').addEventListener('input', function(e) {
  var hour = parseInt(e.target.value);
  // update the map
  map.setFilter('collisions', ['==', ['number', ['get', 'Hour']], hour]);

  // converting 0-23 hour to AMPM format
  var ampm = hour >= 12 ? 'PM' : 'AM';
  var hour12 = hour % 12 ? hour % 12 : 12;

  // update text in the UI
  document.getElementById('active-hour').innerText = hour12 + ampm;
});

```

Here's what it will look like:

{{
  <DemoIframe src="/help/demos/show-changes-over-time/step-three.html" />
}}

## Filter by day of the week

Another useful metric for gathering insights about collisions in NYC is the day of the week when accidents occur. With the following code, you can add radio buttons that filter on days of the week.

### Create a radio button group

First, add the following radio button group in your HTML inside the `console` div.

```html
<div class='session'>
  <h2>Day of the week</h2>
  <div class='row' id='filters'>
    <input id='all' type='radio' name='toggle' value='all' checked='checked'>
    <label for='all'>All</label>
    <input id='weekday' type='radio' name='toggle' value='weekday'>
    <label for='weekday'>Weekday</label>
    <input id='weekend' type='radio' name='toggle' value='weekend'>
    <label for='weekend'>Weekend</label>
  </div>
</div>
```

### Add interactivity

Create a new `change` event listener in your code, like you did for the slider, then place it after the slider event. To show collisions on all days, use a [`!=`](https://www.mapbox.com/mapbox-gl-js/style-spec#expressions-!=) expression that filters for the 'placeholder' value. This filter is added so that `filterDay` never evaluates to null. It will become clearer why this is necessary by the end of the tutorial.

To filter for weekday and weekend values, use a `match` expression. Match expressions allow you to specify input and output values. The pattern that the expression below follows is:

```
['match', ['get', property], inputValue, outputValue if match, outputValue if not a match]
```

Add the following code after the slider event you added in the previous step:

```js
document.getElementById('filters').addEventListener('change', function(e) {
  var day = e.target.value;
  // update the map filter
  if (day === 'all') {
    filterDay = ['!=', ['string', ['get', 'Day']], 'placeholder'];
  } else if (day === 'weekday') {
    filterDay = ['match', ['get', 'Day'], ['Sat', 'Sun'], false, true];
  } else if (day === 'weekend') {
    filterDay = ['match', ['get', 'Day'], ['Sat', 'Sun'], true, false];
  } else {
    console.log('error');
  }
  map.setFilter('collisions', ['all', filterDay]);
});
```

Refresh your page and try the week of the day buttons.

{{
  <DemoIframe src="/help/demos/show-changes-over-time/step-four.html" />
}}

## Combine the filters

As you may have discovered, toggling between weekday and weekend will automatically override the hour filter. You can fix this by using a combining filter ([documentation](https://www.mapbox.com/mapbox-gl-style-spec/#types-filter)).

### Combining filters

To combine multiple filters, you will append them to a new [`'all'`](https://www.mapbox.com/mapbox-gl-js/style-spec#expressions-all) expression. Using this `'all'` expression makes sure that both filters result in true.

Add two variables at the beginning of the map `load` event handler to store the 'hour' and 'day of the week' filters and apply them independently. This way when you want to update one part of the filter, you can update that variable, then apply setFilter(`my layer`, `['all', filterHour, filterDay]`) to reset the filter.

First, add two variables at the beginning of the map `load` event handler you created earlier. This is where the placeholder filter becomes necessary since you cannot have `null` in a combining filter.

```js
var filterHour = ['==', ['number', ['get', 'Hour']], 12];
var filterDay = ['!=', ['string', ['get', 'Day']], 'placeholder'];
```

Then, in `addLayer`, replace the value of `filter` with: `['all', filterHour, filterDay]`.

Next, in the slider `onInput` event, replace `map.setFilter('collisions', ['==', ['number', ['get', 'Hour']], hour]);` with this code:

```js
filterHour = ['==', ['number', ['get', 'Hour']], hour];
map.setFilter('collisions', ['all', filterHour, filterDay]);
```

Lastly, polish the week of the day `onChange` event by replacing it with this code:

```js
document.getElementById('filters').addEventListener('change', function(e) {
  var day = e.target.value;
  if (day === 'all') {
    // `null` would not work for combining filters
    filterDay = ['!=', ['string', ['get', 'Day']], 'placeholder'];
  }
  /* the rest of the if statement */
  map.setFilter('collisions', ['all', filterHour, filterDay]);
});
```

## Finished product

You created a map showing NYC collision data from January 2016, complete with data-driven styles, a legend, a time slider, and a day of the week filter.

{{
  <DemoIframe src="/help/demos/show-changes-over-time/step-five.html" />
}}

## Next steps

With this guide, you have the tools to create your own interactive time series data visualizations with Mapbox GL JS. Explore more Mapbox GL JS resources on our Help page and see the full [Mapbox GL JS documentation](https://www.mapbox.com/mapbox-gl-js) and [examples](https://www.mapbox.com/mapbox-gl-js/examples) for more inspiration and guidance.
