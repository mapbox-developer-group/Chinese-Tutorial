---
title: Add custom icons or markers
description: You can add markers, style them, and add tooltips dynamically with Mapbox GL JS. This overview samples all the ways to add custom, interactive markers.
thumbnail: markers
level: 1
topics:
- web apps
language:
- Varies
prependJs:
  - "import * as constants from '../../constants';"
  - "import Note from '@mapbox/dr-ui/note';"
  - "import BookImage from '@mapbox/dr-ui/book-image';"
  - "import Icon from '@mapbox/mr-ui/icon';"
  - "import DemoIframe from '@mapbox/dr-ui/demo-iframe';"
  - "import { LegacyNote } from '../../components/legacy-note';"
contentType: tutorial
---

There are many different ways to style point data in [Mapbox Studio](https://www.mapbox.com/studio), [Mapbox GL JS](https://www.mapbox.com/mapbox-gl-js/api/), and the Mapbox [iOS](https://www.mapbox.com/ios-sdk) and [Android](https://www.mapbox.com/android-sdk) SDKs. In these tutorials, we’ll walk you through several ways to visualize your point data across platforms with custom icons and markers. There's no one right way to build your map, and this guide is designed to provide you with a better understanding of which methods make the most sense for your project.

## Use the marker playground

Use the [marker playground](/help/interactive-tools/marker-playground/) to add an image marker to the map and view the platform-specific code necessary to recreate this map in your own iOS, Android, or web application.

![screenshot of the marker playground](/help/img/interactive-tools/marker-playground.png)

## Add markers in Mapbox GL JS

If you already have GeoJSON data that you would like to visualize, you can use Mapbox GL JS to add custom markers to your map. When using the Mapbox GL JS Marker method, you can use any file type that can be used as an [image in CSS](https://developer.mozilla.org/en-US/docs/Web/CSS/image) as a marker on your map. To build a custom marker map entirely in Mapbox GL JS, follow the [Add custom markers in Mapbox GL JS](/help/tutorials/custom-markers-gl-js/) tutorial. This tutorial is code-based.

{{
  <DemoIframe src="/help/demos/custom-markers-gl-js/index.html" />
}}

## Add custom icons in Mapbox Studio

If you are starting from scratch and need to draw data to be added to a map, start with the [Add points to a map](/help/tutorials/add-points-pt-1/) tutorial series. In this tutorial series, you'll learn how to draw data from scratch in the Mapbox Studio dataset editor, add custom icons to a map in the Mapbox Studio style editor, and make your map interactive using Mapbox GL JS. Making your map interactive will require writing code.

{{<img src='/help/img/studio/add-points-preview.gif' alt='animation of points in the dataset editor and custom icons in the style editor' style={{ width: "50%" }} className='fr-mm w-full w360-mm pl24-mm' />}}

### Part 1: create a dataset

Learn how to create a new dataset in the Mapbox Studio dataset editor, draw new points, save your dataset, and export it as a tileset. **[Add points to a web map, Part 1: create a dataset {{<Icon name='arrow-right' inline={true} />}}](/help/tutorials/add-points-pt-1)**

### Part 2: create a style

Learn to create a new style with one of the Mapbox default styles, add a tileset as a layer, and style the points with custom icons in the Mapbox Studio style editor. **[Add points to a web map, Part 2: create a style {{<Icon name='arrow-right' inline={true} />}}](/help/tutorials/add-points-pt-2)**

### Part 3: add interactivity

Learn how to use Mapbox GL JS to add popups when each point is clicked. This part requires writing code. **[Add points to a web map, Part 3: add interactivity {{<Icon name='arrow-right' inline={true} />}}](/help/tutorials/add-points-pt-3)**

{{
  <Note
    imageComponent={<BookImage />}
  >
    <p>In this tutorial series you will add custom icons inside Mapbox Studio. Mapbox Studio only supports SVG images. Other image formats are supported when using markers in Mapbox GL JS.</p>
  </Note>
}}

## Add markers in iOS

The Mapbox Maps SDK for iOS offers a few different methods for visualizing point data on your map. Each method has its merits and drawbacks, so be sure to take a quick look, particularly if you expect to add a lot of markers or display highly customized markers.

See the [Adding Points to a Map](https://www.mapbox.com/ios-sdk/maps/overview/markers-and-annotations/) guide for the Mapbox Maps SDK for iOS for more information on how to use the available methods for visualizing point data on your map and to learn about each method's trade-offs.

## Add markers in Android

The [Annotation plugin](https://docs.mapbox.com/android/plugins/overview/annotation) is the recommended way to add markers to a map when using the Maps SDK for Android. The Annotation plugin simplifies the way to set and adjust the visual properties of annotations on a Mapbox map.

[Directly using the Maps SDK for Android's sources and layers](https://docs.mapbox.com/android/maps/overview/data-driven-styling/) instead of the Annotation plugin, is the advanced way to add annotations. 

## Add markers in Mapbox.js

{{
  <LegacyNote
    legacyProduct='Mapbox.js'
    alternativeResource={{
      title: 'Add custom markers in Mapbox GL JS',
      link: '/help/tutorials/custom-markers-gl-js/'
    }}
  />
}}

If you want to know how to add markers with Mapbox.js, read our [Work with markers with Mapbox.js](/help/tutorials/markers-js) guide. In this guide, you will learn how to add markers, customize them, and make them interactive with [Mapbox.js](https://www.mapbox.com/mapbox.js).
