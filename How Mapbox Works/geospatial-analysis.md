---
title: Spatial analysis
description: Learn how spatial analysis with Turf works and how to use Turf in your web application.
image: /img/narrative/analysis.svg
topics:
  - analysis
prependJs:
  - "import DemoIframe from '@mapbox/dr-ui/demo-iframe';"
contentType: guide
---

Spatial analysis includes a variety of techniques and processes used to understand the patterns and relationships of geographic features. [Turf](http://turfjs.org/) is an advanced geospatial JavaScript open source library that allows you to do spatial operations in the browser. Turf helps you analyze, aggregate, and transform data to visualize it in new ways and answer advanced questions. This guide provides an overview of how spatial analysis with Turf works, how to use Turf in your application, and relevant documentation to help you get started.

<div class='bg-white border-b'>
  <div class='txt-m txt-bold'>Perform spatial operations in the browser</div>
  <div class='txt-xs pb6'>Click points on the map to create lines that measure distanced using turf.lineDistance.</div>
</div>

{{
  <DemoIframe src="/help/demos/how-mapbox-works/spatial-analysis.html" />
}}

## How spatial analysis works

[Turf](http://turfjs.org/) is a library for **geospatial analysis** &mdash; a large family of tasks like _calculating area and distance_ and _joining points to polygons_ that enable people to see patterns or relationships within their data. Spatial analysis is used in many industries: to find the [nearest coffee shop](https://www.mapbox.com/blog/coffee-with-turf/), [calculate travel time](https://www.mapbox.com/blog/playback-the-iditarod-with-turf/), and show [regional statistics for utility usage](https://www.mapbox.com/blog/turf-government-data/). It's also a huge part of GIS, where many problems are solved with spatial analysis.

### Examples of spatial analysis

<div class='fr pl12' style='width:50%'>
  <img alt='map of 1854 cholera outbreak in London' src='/help/img/screenshots/snow-cholera-map-1.jpg' />
  <p class='caption'><strong>Source</strong>: John Snow - Published by C.F. Cheffins, Lith, Southhampton Buildings, London, England, 1854 in Snow, John. On the Mode of Communication of Cholera, 2nd Ed, John Churchill, New Burlington Street, London, England, 1855.</p>
</div>

The map below is a classic example of spatial analysis, created by physician John Snow during the 1854 cholera outbreak in London. Snow [plotted](http://en.wikipedia.org/wiki/1854_Broad_Street_cholera_outbreak) cholera cases in the Soho area of London around Broad Street and noticed a cluster around the water pump. This led to improved sanitation facilities and the discovery that cholera infection was water-borne rather than airborne.

Today, spatial analysis is used in epidemiology, biology, statistics, economics, commerce and business, urban planning, geology, oil and gas, and in [many other industries](https://www.mapbox.com/industries/). With Turf, we can now bring these analyses to the browser and show results quickly and seamlessly.

### Common functions

There are dozens of functions available within Turf that allow you to do spatial operations with your data. Some of the most common operations are:

- **Buffer**: returns an area that is a specified number of units around your feature.
- **Inside**: returns whether a feature is wholly within an area.
- **Area**: calculates the area of a polygon.
- **Along**: returns the position of a point at a specified distance along a line.

A typical Turf operation such as the **buffer** function would look like this in JavaScript:

```js
var nullIsland = {
  type: 'Feature',
  geometry: {
    type: 'Point',
    coordinates: [0, 0]
  },
  properties: {
    name: 'Null Island'
  }
};

var twoHundredMilesOut = turf.buffer(nullIsland, 200, { unit: 'miles' });

```

{{
  <DemoIframe src="/help/demos/turf-intro/nullisland.html" />
}}

### Method types

There are several different kinds of spatial analysis you can conduct with Turf. All Turf methods are organized into the following categories:

- **Aggregation methods** can run statistical operations on a set of points within a set of polygons. For example, you can compare average size of elementary schools across counties in Massachusetts with [turf-collect](http://turfjs.org/docs#collect).

- **Measurement methods** can measure distances, create features, and calculate sizes. For example, with measurement methods, you can determine not only the exact center point of the city of Austin (with [turf-centroid](http://turfjs.org/docs#centroid), but you can also measure the distance between that point and city hall (with [turf-distance](http://turfjs.org/docs#distance)).

- **Transformation methods** can solve spatial problems. If you want to buy a house that is both within one mile of a park and one mile of a bus stop, you can determine where those areas overlap with [turf-intersect](http://turfjs.org/docs#intersect), a transformation method.

- **Data methods** can generate random points or samples from a large number of features *at random*. For example, you can use [turf-sample](http://turfjs.org/docs#sample) to list a subset of store locations from hundreds of locations.

- **Interpolation methods** can estimate or average data and visualize the result. For example, creating contour lines (or isobands) from a set of points containing elevation information with [Turf isobands](http://turfjs.org/docs#isolines).

- **Join methods** can determine spatial relationships between features. If you want to know which burglaries happened in a specific neighborhood, you can use a join method like [turf-within](http://turfjs.org/docs#within).


## Using spatial analysis

As a JavaScript library, you can add [Turf](http://turfjs.org/) to your webpage in the `<head>` of your document. You can use the CDN (the URL displayed below), or you can [download the Turf library](http://turfjs.org/) and source it locally.

```html
<script src='https://npmcdn.com/@turf/turf/turf.min.js'></script>
```

When you add Turf to your site, it exposes a global variable `turf` from which you can run any of the [turf functions](http://turfjs.org/docs). For example, if you have a GeoJSON LineString feature named `dc` and you want to know its length in miles, you can use the [turf-length](http://turfjs.org/docs#length) function.

```js
var dc = {
  type: 'Feature',
  properties: {},
  geometry: {
    type: 'LineString',
    coordinates: [
      [-77.031669, 38.878605],
      [-77.029609, 38.881946],
      [-77.020339, 38.884084],
      [-77.025661, 38.885821],
      [-77.021884, 38.889563],
      [-77.019824, 38.892368]
    ]
  }
};

var length = turf.length(dc, { units: 'miles' });
```

{{
  <DemoIframe src="/help/demos/turf-intro/linestring.html" />
}}

The variable `length` contains the length of `dc` in miles.

```js
// length === 1.6389817168470033
```

You can find a complete list of available functions and see them in action in the [Turf API documentation](http://turfjs.org/docs).
