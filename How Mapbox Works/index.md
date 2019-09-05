---
title: Overview
description: Learn about the building blocks that Mapbox provides so you can create custom mapping applications.
headerImage: /help/img/categories/guide.svg
color: cyan
prependJs:
  - "import constants from '../../constants.json';"
  - "import ChevronousText from '@mapbox/mr-ui/chevronous-text';"
  - "import DemoIframe from '@mapbox/dr-ui/demo-iframe';"
  - "import { DemoStatic } from '../../components/demo-static';"
  - "import { HmwMapSources } from '../../components/diagrams/hmw-map-sources';"
  - "import GLWrapper from '@mapbox/dr-ui/gl-wrapper';"
contentType: guide
contentTypeTitle: How Mapbox works
---

Welcome to Mapbox! Mapbox is a developer platform used [across industries](https://www.mapbox.com/industries) to create custom applications that solve problems with maps, data, and spatial analysis. Mapbox's tools are building blocks that support every part of the web and mobile map-making process. Whether your goal is to build a beautiful map to match your website or to build a full-featured geoprocessing application, we have you covered.

These guides will introduce you to the building blocks of Mapbox and how you can:

- Work with in Mapbox's **robust data**.
- **Style** your map down to the smallest details.
- **Upload** or **create** custom data.
- **Develop** full-featured web and mobile applications.
- **Extend** your app's functionality with web services for [geocoding](/help/glossary/geocoding/), directions, spatial analysis, and more.
- **Create** static maps programmatically.

## Use Mapbox map data

{{
  <GLWrapper><HmwMapSources /></GLWrapper>
}}

Our core [tilesets](/help/glossary/tileset/): Mapbox Streets, Mapbox Terrain, Mapbox Traffic, and Mapbox Satellite. Each tileset contains a unique set of data from a variety of sources.

- **Mapbox Streets** includes streets, buildings, administrative areas, water, and land data based on [OpenStreetMap](http://www.openstreetmap.org/), updated as often as every five minutes.
- **Mapbox Terrain** includes landcover data and a worldwide elevation data set complete with contours, hillshade, and elevation data.
- **Mapbox Satellite**  includes global satellite imagery from [a range of sources](https://www.mapbox.com/about/maps), processed and seamed together by Mapbox.
- **Mapbox Traffic** includes regularly updated vehicle congestion information on top of Mapbox Streets.

You can find a full list of layers available in the Mapbox Streets, Terrain, and Traffic sources in our [Vector Tiles overview](https://www.mapbox.com/vector-tiles/). You can read more about our data sources on our [Maps page](https://www.mapbox.com/about/maps).

<a className="txt-bold" href="/help/how-mapbox-works/mapbox-data/">{{<ChevronousText text="Learn about our data" />}}</a>

## Design a map

Custom map design is one of the core functions of Mapbox Studio. We provide an advanced application for putting this customization at your fingertips with the Mapbox Studio style editor. In Mapbox Studio, you can start with one of our [template styles](https://www.mapbox.com/maps/) or [designer styles](https://www.mapbox.com/designer-maps/) and style each individual layer to your exact specification.

{{
  <DemoIframe src="/help/demos/how-mapbox-works/map-design.html" />
}}

On the left you can see the **Basic style**, a template style made up of a limited set of layers. On the right you can see a **custom style** that uses all the same underlying data, but that has been customized by changing colors and fonts in Mapbox Studio style editor.

The [Mapbox Studio style editor](https://www.mapbox.com/studio/styles) is a full-featured map editor that gives you total control over the style of your map directly in your browser. Whether you start with a Mapbox template style or start from scratch, the styling possibilities are virtually endless. With the Mapbox Studio style editor, you can:

- Create styles that change dynamically based on zoom level.
- Use custom fonts.
- Set custom alignment, pitch, offset, and more for your labels.
- Set colors, weights, and opacity for your map layers.
- Filter tilesets based on attributes.

<a className="txt-bold" href="/help/how-mapbox-works/map-design/">{{<ChevronousText text="Learn about map design" />}}</a>

## Add custom data

Mapbox provides robust geospatial data with our Streets, Terrain, Traffic, and Satellite tilesets, but mapping applications often require custom data. To add custom data to your map, you can upload your own data as [tilesets](/help/glossary/tileset) or create [datasets](/help/glossary/dataset).

**Tilesets and datasets are two different types of data**: tilesets are styleable and datasets are editable. Styling includes changing things like color, opacity, font, or icon. Editing includes changing the placement of features (points, lines, polygons), their geometries, and adding or deleting features from a feature collection. If you have created or imported a dataset, you can export your dataset to a tileset right in Mapbox Studio and use it in the Mapbox Studio style editor like you would any other tileset.

### Upload tilesets

Tilesets are lightweight collections of vector data that are optimized for rendering and are not editable. When you [upload custom data](/help/troubleshooting/uploads), your files are converted to vector tilesets, which can be styled in the Mapbox Studio style editor, added to [interactive web maps with Mapbox GL JS](https://www.mapbox.com/mapbox-gl-js/example/queryrenderedfeatures/), and used in mobile applications created with the Mapbox Maps SDKs for [iOS](https://docs.mapbox.com/ios/maps/overview/) and [Android](https://docs.mapbox.com/android/maps/overview/).

For more details about accepted file types and methods for uploading data, see the [Uploading data guide](/help/how-mapbox-works/uploading-data/).

<a className='txt-bold' href="/help/how-mapbox-works/uploading-data/">{{<ChevronousText text="Learn about uploads" />}}</a>

### Create datasets

A dataset is an editable collection of [GeoJSON features](https://tools.ietf.org/html/rfc7946). A feature stored with Mapbox has both geometries and properties (attributes), both of which can be edited in the Mapbox Studio dataset editor or through the Mapbox Datasets API. You can use the [dataset editor](https://www.mapbox.com/studio-manual/reference/datasets) in Mapbox Studio to import, create, and edit GeoJSON point, line, and polygon features and their properties. Once you've finished working with your dataset, you can export it to a tileset for use with the Mapbox Studio [style editor](https://www.mapbox.com/studio/). There are limits to how much data you can load into the Mapbox Studio dataset editor at a time, but you can use the Mapbox [Datasets API](https://docs.mapbox.com/api/maps/#datasets) to add more features and manage them programmatically.

<img alt="animated GIF demonstrating how to modify a feature in the Mapbox studio dataset editor" className='px0 py0 mx0 my0' src="/help/img/studio/dataset-modify-feature.gif" />

For more details about accepted file types and methods for creating datasets, see the [Creating new data guide](/help/how-mapbox-works/creating-data/).


<a className='link txt-ms txt-bold' href="/help/how-mapbox-works/creating-data/">{{<ChevronousText text="Learn about creating data" />}}</a>

## Build applications

Once you've created, styled, and added data to your map, Mapbox provides multiple tools for integrating your maps into a website or custom application.

### Web applications

You can use one of our JavaScript libraries to publish your map to the web.

{{
  <DemoIframe src="/help/demos/gl-store-locator/step-five.html" />
}}


This web application uses a combination of HTML, CSS, JavaScript, and  **Mapbox GL JS**, our WebGL-based JavaScript library. If you are interested in learning more about how to build an application like this one, read our step-by-step [Build a store locator](/help/tutorials/building-a-store-locator/) tutorial.


[Mapbox GL JS](https://www.mapbox.com/mapbox-gl-js/) is a JavaScript library for creating interactive, customizable maps from Mapbox styles and vector tiles. Mapbox GL JS uses WebGL, a technology used to create video games in the browser, which enables you to build advanced interactions into your maps, including smooth zooming, map bearing and pitch, querying underlying map data, and dynamically filtering the data you choose to display. You can use the custom styles you've created in the Mapbox Studio style editor or any of the template styles we provide, plus add any additional data you want programmatically -- including GeoJSON, images, and even [video](https://www.mapbox.com/mapbox-gl-js/example/video-on-a-map/)! Be sure to explore the [Mapbox GL JS examples](https://www.mapbox.com/mapbox-gl-js/examples) for dozens of other interactive examples.

[Mapbox.js](https://www.mapbox.com/mapbox.js/) is our older JavaScript web mapping library that extends the popular [Leaflet.js](http://leafletjs.com) library. Mapbox.js can be used to create interactive maps with [classic styles](/help/glossary/classic-style/).


<a className="txt-bold" href="/help/how-mapbox-works/web-apps">{{<ChevronousText text="Learn about web apps" />}}</a>


### Mobile applications

Mapbox provides a Maps SDK for [iOS](https://www.mapbox.com/ios-sdk/) and [Android](https://www.mapbox.com/android-docs/) for publishing your maps in native applications. The Maps SDKs for iOS and Android are designed to be drop-in replacements for Apple's MapKit and the Google Maps SDKs. The Maps SDKs should be familiar to mobile developers who have experience with either. Often, your maps can be swapped for Mapbox by changing a single line of code.

![Mapbox maps on a mobile device](/help/img/screenshots/mobile.png)

Each SDK comes bundled with five Mapbox-designed map styles and can handle any custom design created with the [Mapbox Studio style editor](https://www.mapbox.com/studio/). If you use one of Mapbox's mobile SDKs, you'll also get access to the [mobile usage dashboard](https://www.mapbox.com/account/statistics), which provides a continuously updated view of monthly active users, map usage, and region-by-region metrics.


<a className="txt-bold" href="/help/how-mapbox-works/mobile-apps/">{{<ChevronousText text="Learn about mobile apps" />}}</a>



### Unity applications

![Mapbox SDK for Unity sample image](/help/img/unity/games.jpg)

Mapbox makes real world simulations possible by giving you the tools to put real world maps in your Unity applications. The [Mapbox Maps SDK for Unity](/help/glossary/mapbox-maps-sdk-for-unity/) is a set of tools to build Unity applications from real map data. It consists of a robust API for interfacing with Mapbox web services and converting map resources into game objects as well as a robust graphical user interface built on top of the Unity platform.


<a className="txt-bold" href="/help/how-mapbox-works/unity/">{{<ChevronousText text="Learn about Unity apps" />}}</a>


## Extend your application

Besides designing maps and publishing mapping applications, Mapbox also has tools for interacting with data, locating addresses, conducting spatial analysis, and routing. Our web services APIs are building blocks you can use to make your maps interactive and dynamic.

### Mapbox Geocoding API

Add global place search to your app with the [Mapbox Geocoding API](https://docs.mapbox.com/api/search/#geocoding). Turn latitude and longitude values into addresses with **reverse geocoding** or you turn addresses into latitude and longitude values with **forward geocoding**. You can use the Geocoding API right in your web or mobile application or as a standalone service.


![animation demonstrating geocoding with autocomplete](/help/img/api/geocode.gif)

<a className="txt-bold" href="/help/how-mapbox-works/geocoding/">{{<ChevronousText text="Learn about geocoding" />}}</a>

### Mapbox Directions API

The Mapbox [Directions API](https://docs.mapbox.com/api/navigation/#directions) provides point-to-point directions for walking, cycling, or driving based on the wide network of roads and paths in OpenStreetMap. The Directions API returns text instructions, alternative routes, geometry (for drawing routes), and maneuvers. The Directions API also powers our [Map matching](https://docs.mapbox.com/api/navigation/#map-matching), [Matrix](https://docs.mapbox.com/api/navigation/#matrix), and [Optimization](https://docs.mapbox.com/api/navigation/#optimization) APIs. See the [Directions API documentation](https://docs.mapbox.com/api/navigation/#directions) for more information.

![screenshot of the Mapbox GL JS directions plugin on a map](/help/img/directions/gljs-plugin.png)

<a className="txt-bold" href="/help/how-mapbox-works/directions">{{<ChevronousText text="Learn about directions" />}}</a>

### Analyze with Turf.js

[Turf.js](http://turfjs.org/) is an open source JavaScript library for spatial analysis. Turf includes traditional spatial analysis operations, helper functions for creating GeoJSON data, and data classification and statistics tools. You can add Turf to your website as a client-side plugin, or you can run Turf server-side with Node.js.

![screenshot of a Turf example](/help/img/turf/turf.png)

<a className="txt-bold" href="/help/how-mapbox-works/geospatial-analysis/">{{<ChevronousText text="Learn about analysis" />}}</a>


## Use satellite imagery

Mapbox Satellite is a global basemap of continuous satellite and aerial imagery that you can use as a blank canvas or an overlay for your own data. Comprised of multiple imagery sources, we color correct it and update it as new imagery becomes available.

![samples of Mapbox satellite imagery](/help/img/satellite/satellite.png)

Mapbox Satellite uses global satellite and aerial imagery from commercial providers, NASA, and USGS. As cities grow and landscapes change, we add newer, clearer, and more attractive imagery.

The current zoom level offerings include:

- 0–8: MODIS 2012–2013.
- 9–12: Landsat 5 & 7, 2010–2011.
- 13–19: a combination of open and proprietary sources, including DigitalGlobe’s GBM 2011+ for much of the world, USDA’s NAIP 2011–2013 in the contiguous United States, and open aerial imagery from Denmark, Finland, and parts of Germany.


<a className="txt-bold" href="/help/how-mapbox-works/satellite-imagery/">{{<ChevronousText text="Learn about satellite imagery" />}}</a>


## Create static maps

The Mapbox [Static Images API](https://docs.mapbox.com/api/maps/#static-images) can generate static images from your map styles. Provide your style ID, access token, and a few more parameters &mdash; such as zoom, bearing, pitch, and overlay &mdash; and you can display static images directly by making requests in your application.

{{
  <DemoStatic src="https://api.mapbox.com/styles/v1/mapbox/streets-v{constants.VERSION_STREETS_STYLE}/static/pin-s-a+9ed4bd(-122.46589,37.77343),pin-s-b+000(-122.42816,37.75965),path-5+f44-0.5(%7DrpeFxbnjVsFwdAvr@cHgFor@jEmAlFmEMwM_FuItCkOi@wc@bg@wBSgM)/auto/800x300@2x?access_token=MapboxAccessToken" alt="static Mapbox map with route and point overlays" />
}}

<a className="txt-bold" href="/help/how-mapbox-works/static-maps/">{{<ChevronousText text="Learn about static maps" />}}</a>


## Add attribution

Whether you're creating a custom style with Mapbox Studio or building a mobile app with the Android SDK, all Mapbox tools require [attribution](/help/how-mapbox-works/attribution) according to our [terms of service](https://www.mapbox.com/tos).

<a className="txt-bold" href="/help/how-mapbox-works/attribution">{{<ChevronousText text="Learn about attribution" />}}</a>
